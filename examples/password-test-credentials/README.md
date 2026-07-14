# Secure Test Credentials

Generate real-entropy passwords for staging accounts, test users, and CI secrets — never `Password123!` again.

## Workflow

1. Use the YoBox Password Generator in the browser for one-off credentials.
2. For programmatic use, generate credentials with the Web Crypto API in your test setup.
3. Store them in your CI secret manager, not in `.env` files.

## Snippet — Web Crypto in Node / browser

```js
export function securePassword(length = 24) {
  const alphabet = "ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnpqrstuvwxyz23456789!@#$%^&*";
  const bytes = new Uint8Array(length);
  crypto.getRandomValues(bytes);
  return Array.from(bytes, (b) => alphabet[b % alphabet.length]).join("");
}
```

## Snippet — Cypress test setup

```js
before(() => {
  const password = securePassword(32);
  cy.wrap(password).as("password");
  cy.task("db:createUser", { email: "qa@example.com", password });
});
```

## Do

- Rotate CI test credentials on every deploy.
- Use >=24 chars for anything hitting a real service.
- Log the *fact* a password was used, never the password itself.

## Don't

- Reuse the same "test password" across environments.
- Store secrets in Git, even for staging.
- Use `Math.random()` — it is not cryptographically secure.

## Like this example?

⭐ Star the repository:
https://github.com/hocineman4/yobox-examples

🌐 More developer tools:
https://yobox.dev

## Links

- Tool: [YoBox Password Generator](https://yobox.dev/tools/password-generator?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
- Guide: [Secure Test Credentials with the YoBox Password Generator](https://yobox.dev/blog/secure-test-credentials-with-the-yobox-password-generator?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
