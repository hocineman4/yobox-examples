# Postman Webhook Testing Example

Drive real webhook flows from a Postman collection with YoBox capture endpoints. No mocking, no ngrok.

## Workflow

1. Pre-request script mints a fresh YoBox webhook token and stores its URL in a collection variable.
2. Main request triggers your app to send an outgoing webhook to that URL.
3. Test script polls the YoBox API and asserts on the captured payload.
4. (Optional) Teardown revokes the token when the collection finishes.

## API endpoints used

- `POST   https://api.yobox.dev/webhook/token` — mint a new webhook token/uuid
- `GET    https://api.yobox.dev/webhook/:uuid` — list captured requests
- `ALL    https://api.yobox.dev/webhook/:uuid/*` — public capture URL your app posts to
- `DELETE https://api.yobox.dev/webhook/token/:uuid` — revoke the token

> Field names below are conceptual — adapt them to the live API response.

## Pre-request script

```js
pm.sendRequest(
  { url: "https://api.yobox.dev/webhook/token", method: "POST" },
  (err, res) => {
    const token = res.json();
    pm.collectionVariables.set("hook_uuid", token.uuid);
    pm.collectionVariables.set("hook_url", `https://api.yobox.dev/webhook/${token.uuid}`);
  }
);
```

## Test script

```js
setTimeout(() => {
  const uuid = pm.collectionVariables.get("hook_uuid");
  pm.sendRequest(`https://api.yobox.dev/webhook/${uuid}`, (err, res) => {
    const requests = res.json();
    pm.test("webhook received", () => pm.expect(requests.length).to.be.above(0));
    pm.test("payload has event type", () => {
      pm.expect(requests[0].body).to.have.property("type");
    });
  });
}, 3000);
```

## Teardown (optional)

```js
const uuid = pm.collectionVariables.get("hook_uuid");
pm.sendRequest({ url: `https://api.yobox.dev/webhook/token/${uuid}`, method: "DELETE" });
```

## Links

- Tool: [YoBox Webhook Tester](https://yobox.dev/webhook?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
- Guide: [Testing APIs with Postman + YoBox](https://yobox.dev/blog/testing-api-responses-with-postman-and-yobox?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
