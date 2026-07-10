# YoBox — The Developer Toolbox for Testing, QA & Automation

> Disposable email, webhook capture, regex, mock data, secure passwords, Docker recipes, and framework guides for Cypress, Playwright, and Postman — all in one place, all free, no signup.

**Website:** [yobox.dev](https://yobox.dev/?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)
**Blog:** [yobox.dev/blog](https://yobox.dev/blog?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)

---

## What is YoBox?

YoBox is a collection of fast, browser-based developer tools designed for the boring-but-critical parts of shipping software: testing signup flows, capturing webhooks, generating realistic mock data, validating regex, spinning up Docker builders, and creating secure test credentials.

Every tool works without an account, runs in the browser, and is built to slot directly into your existing CI/CD pipeline, Cypress spec, Playwright fixture, or Postman collection.

## Who is it for?

- **QA engineers** who need disposable inboxes and webhook endpoints for end-to-end tests
- **Backend developers** debugging outgoing webhooks without ngrok or port-forwarding
- **Frontend developers** who need realistic mock data for demos and Storybook
- **DevOps engineers** building reproducible Docker CI images
- **Anyone** who has ever needed a throwaway email or a random secure password

## Tools

| Tool | What it does | Link |
|------|--------------|------|
| Temp Mail | Instant disposable inboxes with API access | [Open](https://yobox.dev/?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |
| Webhook Tester | Public URLs to capture, inspect, and replay webhooks | [Open](https://yobox.dev/webhook?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |
| Docker Builder | Compose recipes and CI-ready Docker patterns | [Open](https://yobox.dev/tools/docker-builder?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |
| Regex Assistant | Test, explain, and generate regex patterns | [Open](https://yobox.dev/tools/regex-assistant?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |
| Password Generator | Cryptographically secure passwords in the browser | [Open](https://yobox.dev/tools/password-generator?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |
| Lorem / Mock Data | Realistic fake data for Cypress, Playwright, Postman | [Open](https://yobox.dev/tools/lorem-ipsum?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |
| Cypress Guide | End-to-end email & webhook testing in Cypress | [Open](https://yobox.dev/tools/cypress?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |
| Playwright Guide | Parallel-safe fixtures with disposable inboxes | [Open](https://yobox.dev/tools/playwright?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |
| Postman Guide | API testing workflows with YoBox endpoints | [Open](https://yobox.dev/tools/postman?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth) |

## Use cases

- **Signup / OTP flows** — Register with a disposable inbox, poll for the magic-link email, verify end-to-end in Cypress or Playwright.
- **Webhook debugging** — Point Stripe, GitHub, or Shopify at a YoBox webhook URL, inspect payloads live, then replay them locally.
- **API contract testing** — Drive Postman collections against real inboxes and captured webhooks with zero mocking.
- **Docker CI** — Copy-paste Compose files that run headless browsers, Redis, and Postgres for every PR.
- **Regex validation** — Prototype patterns for email, phone, and log parsing before shipping them into production.
- **Secure test credentials** — Generate passwords for staging accounts with real entropy, not `Password123!`.

## Working examples

Ready-to-run examples live under [`/examples`](./examples):

- [cypress-signup-otp](./examples/cypress-signup-otp) — magic-link signup with a per-test inbox
- [playwright-email-webhooks](./examples/playwright-email-webhooks) — parallel-safe Playwright fixtures
- [postman-webhook-testing](./examples/postman-webhook-testing) — capture and assert webhooks in Postman
- [docker-e2e-testing](./examples/docker-e2e-testing) — Compose stack for headless E2E in CI
- [regex-qa-patterns](./examples/regex-qa-patterns) — battle-tested regex snippets for QA
- [password-test-credentials](./examples/password-test-credentials) — secure credential generation for tests

## Recommended reading

Deep guides from the YoBox blog:

- [The Complete Cypress Guide](https://yobox.dev/blog/cypress-e2e-with-yobox-disposable-email-and-webhook-tester?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)
- [Playwright + YoBox: Parallel-Safe End-to-End Testing](https://yobox.dev/blog/playwright-automation-with-yobox-end-to-end-email-and-webhooks?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)
- [Testing APIs with Postman + YoBox](https://yobox.dev/blog/testing-api-responses-with-postman-and-yobox?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)
- [Webhook Testing Without ngrok](https://yobox.dev/blog/webhook-testing-without-ngrok?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)
- [The Only Docker Compose Pattern You Need](https://yobox.dev/blog/the-only-docker-compose-pattern-you-need?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)
- [10 Regex Patterns Every QA Engineer Should Memorize](https://yobox.dev/blog/regex-patterns-every-qa-engineer-should-memorize?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)
- [Realistic Mock Data for Cypress, Playwright & Postman](https://yobox.dev/blog/realistic-mock-data-for-cypress-playwright-and-postman?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)
- [Secure Test Credentials with the YoBox Password Generator](https://yobox.dev/blog/secure-test-credentials-with-the-yobox-password-generator?utm_source=github&utm_medium=readme&utm_campaign=yobox_growth)

## How this repo helps you

See [`docs/github-growth.md`](./docs/github-growth.md) for the philosophy behind the examples and how YoBox uses GitHub to help developers test real workflows end-to-end.

## License

Examples in this repository are MIT licensed — copy, adapt, and ship.
