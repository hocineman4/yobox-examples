# Docker E2E Testing Example

A minimal Docker Compose stack for running headless Playwright or Cypress against a full app in CI. Copy the compose file, tweak the service names, ship.

## Workflow

1. `docker compose up --build --abort-on-container-exit` boots the app, db, and the test runner.
2. The runner waits for the app healthcheck, then executes E2E specs against the disposable stack.
3. Tests hit YoBox for disposable inboxes and webhook URLs — no external accounts.
4. Exit code from the runner becomes the CI job's exit code.

## docker-compose.e2e.yml

```yaml
services:
  app:
    build: .
    environment:
      DATABASE_URL: postgres://postgres:postgres@db:5432/app
    depends_on: [db]
    healthcheck:
      test: ["CMD", "wget", "-qO-", "http://localhost:3000/health"]
      interval: 5s
      retries: 20

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_PASSWORD: postgres

  e2e:
    image: mcr.microsoft.com/playwright:v1.48.0-jammy
    working_dir: /work
    volumes: ["./:/work"]
    command: sh -c "npx wait-on http://app:3000/health && npx playwright test"
    depends_on:
      app:
        condition: service_healthy
```

## GitHub Actions

```yaml
- run: docker compose -f docker-compose.e2e.yml up --build --abort-on-container-exit --exit-code-from e2e
```
## Like this example?

⭐ Star the repository:
https://github.com/hocineman4/yobox-examples

🌐 More developer tools:
https://yobox.dev

## Links

- Tool: [YoBox Docker Builder](https://yobox.dev/tools/docker-builder?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
- Guide: [The Only Docker Compose Pattern You Need](https://yobox.dev/blog/the-only-docker-compose-pattern-you-need?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
