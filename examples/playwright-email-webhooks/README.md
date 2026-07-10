# Playwright Email + Webhooks Example

Per-test disposable inbox and webhook URL as Playwright fixtures. Parallel-safe because every worker gets its own YoBox resources.

## Workflow

1. Fixture requests a fresh inbox and webhook token from YoBox.
2. Your spec drives the app to trigger email + webhook events.
3. Assert on delivered emails and captured webhook payloads.
4. Fixture teardown revokes the webhook token; inboxes expire on their own.

## API endpoints used

Temp Mail:

- `POST   https://api.yobox.dev/mail/account` — create inbox (returns address + token)
- `GET    https://api.yobox.dev/mail/messages` — list messages (authenticated)
- `GET    https://api.yobox.dev/mail/messages/:id` — fetch a single message

Webhook:

- `POST   https://api.yobox.dev/webhook/token` — mint a new webhook token/uuid
- `GET    https://api.yobox.dev/webhook/:uuid` — list captured requests
- `ALL    https://api.yobox.dev/webhook/:uuid/*` — the public URL your app posts to
- `DELETE https://api.yobox.dev/webhook/token/:uuid` — revoke the token

> Treat the snippet below as a conceptual template — response field names should be adapted to the live API.

## Snippet (conceptual)

```ts
// tests/fixtures.ts
import { test as base, request } from "@playwright/test";

type YoBox = {
  inbox: { address: string; token: string };
  hook: { uuid: string; url: string };
};

const API = "https://api.yobox.dev";

export const test = base.extend<YoBox>({
  inbox: async ({}, use) => {
    const api = await request.newContext();
    const inbox = await (await api.post(`${API}/mail/account`)).json();
    await use(inbox);
  },
  hook: async ({}, use) => {
    const api = await request.newContext();
    const token = await (await api.post(`${API}/webhook/token`)).json();
    const hook = { uuid: token.uuid, url: `${API}/webhook/${token.uuid}` };
    await use(hook);
    await api.delete(`${API}/webhook/token/${token.uuid}`);
  },
});
export { expect } from "@playwright/test";
```

```ts
// tests/checkout.spec.ts
import { test, expect } from "./fixtures";
import { request } from "@playwright/test";

const API = "https://api.yobox.dev";

test("stripe webhook + receipt email", async ({ page, inbox, hook }) => {
  await page.goto(`/checkout?email=${inbox.address}&webhook=${encodeURIComponent(hook.url)}`);
  await page.click("text=Pay");

  const api = await request.newContext();

  // Webhook delivered to https://api.yobox.dev/webhook/:uuid/*
  await expect
    .poll(async () => (await (await api.get(`${API}/webhook/${hook.uuid}`)).json()).length)
    .toBeGreaterThan(0);

  // Receipt email delivered to the disposable inbox
  await expect
    .poll(async () => {
      const res = await api.get(`${API}/mail/messages`, {
        headers: { Authorization: `Bearer ${inbox.token}` },
      });
      const body = await res.json();
      return body.messages?.length ?? 0;
    })
    .toBeGreaterThan(0);
});
```

## Links

- Tools: [Temp Mail](https://yobox.dev/?utm_source=github&utm_medium=example&utm_campaign=yobox_growth) · [Webhook Tester](https://yobox.dev/webhook?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
- Guide: [Playwright + YoBox: Parallel-Safe E2E Testing](https://yobox.dev/blog/playwright-automation-with-yobox-end-to-end-email-and-webhooks?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
