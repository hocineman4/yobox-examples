# How YoBox Uses GitHub to Help Developers Test Real Workflows

YoBox is a browser-based toolbox, but the hard problems it solves — signup flows, webhook debugging, mock data, secure credentials — all live inside developer codebases. This repository exists to close that gap: every YoBox tool has a matching, runnable example here that you can lift straight into your own project.

## The philosophy

Documentation tells you what a tool does. Examples show you how it fits into the work you're actually doing on a Tuesday afternoon at 3pm when a flaky test is blocking a release. This repo is optimized for the second case.

Each example is:

- **Small** — one folder, one problem, one working snippet.
- **Copy-pasteable** — no build system, no framework lock-in.
- **Linked back** — every example points to the matching YoBox tool and the long-form blog guide that explains the "why".

## What you'll find here

| Area | Example | YoBox tool |
|------|---------|------------|
| Disposable email testing | [cypress-signup-otp](../examples/cypress-signup-otp) | [Temp Mail](https://yobox.dev/?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth) |
| Webhook inspection | [playwright-email-webhooks](../examples/playwright-email-webhooks), [postman-webhook-testing](../examples/postman-webhook-testing) | [Webhook Tester](https://yobox.dev/webhook?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth) |
| API testing | [postman-webhook-testing](../examples/postman-webhook-testing) | [Postman Guide](https://yobox.dev/tools/postman?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth) |
| QA automation | [cypress-signup-otp](../examples/cypress-signup-otp), [playwright-email-webhooks](../examples/playwright-email-webhooks) | [Cypress](https://yobox.dev/tools/cypress?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth) / [Playwright](https://yobox.dev/tools/playwright?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth) |
| Docker CI workflows | [docker-e2e-testing](../examples/docker-e2e-testing) | [Docker Builder](https://yobox.dev/tools/docker-builder?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth) |
| Regex validation | [regex-qa-patterns](../examples/regex-qa-patterns) | [Regex Assistant](https://yobox.dev/tools/regex-assistant?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth) |
| Secure test credentials | [password-test-credentials](../examples/password-test-credentials) | [Password Generator](https://yobox.dev/tools/password-generator?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth) |

## Why GitHub

GitHub search is where developers land when they're mid-problem. A README with a working Playwright fixture that uses a disposable inbox is worth more than a landing page — it's the shortest path from "I have a flaky signup test" to "I have a green build".

If any of the examples save you time, star the repo and share it with your team. If something's missing, open an issue — the roadmap is driven by real testing pain.

## Learn more on the YoBox blog

- [The Complete Cypress Guide](https://yobox.dev/blog/cypress-e2e-with-yobox-disposable-email-and-webhook-tester?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth)
- [The Complete Playwright Guide](https://yobox.dev/blog/playwright-automation-with-yobox-end-to-end-email-and-webhooks?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth)
- [Testing APIs with Postman + YoBox](https://yobox.dev/blog/testing-api-responses-with-postman-and-yobox?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth)
- [Webhook Testing Without ngrok](https://yobox.dev/blog/webhook-testing-without-ngrok?utm_source=github&utm_medium=docs&utm_campaign=yobox_growth)
