# Cypress Signup + OTP Example

End-to-end test for a magic-link signup flow using a fresh YoBox disposable inbox per test — parallel-safe, no shared state.

## Workflow

1. Create a new inbox via the YoBox API.
2. Submit the signup form with that address.
3. Poll the inbox for the magic-link email.
4. Extract the link, visit it, assert the user is signed in.

## API endpoints used

- `POST https://api.yobox.dev/mail/account` — provision a disposable inbox (returns an address and access token).
- `GET  https://api.yobox.dev/mail/messages` — list messages for the authenticated inbox.
- `GET  https://api.yobox.dev/mail/messages/:id` — fetch a single message (headers, html, text).

> The exact request/response shape is documented at [yobox.dev](https://yobox.dev/?utm_source=github&utm_medium=example&utm_campaign=yobox_growth). Treat the snippet below as a conceptual template — adapt field names to the live API response.

## Snippet (conceptual)

```js
// cypress/e2e/signup.cy.js
describe("signup magic link", () => {
  it("delivers and verifies", () => {
    // 1. Create a disposable inbox
    cy.request("POST", "https://api.yobox.dev/mail/account").then(({ body: inbox }) => {
      const authHeaders = { Authorization: `Bearer ${inbox.token}` };

      // 2. Submit the signup form
      cy.visit("/signup");
      cy.get("input[name=email]").type(inbox.address);
      cy.get("button[type=submit]").click();

      // 3. Poll the inbox until a message arrives
      cy.waitUntil(
        () =>
          cy
            .request({ url: "https://api.yobox.dev/mail/messages", headers: authHeaders })
            .then((r) => r.body.messages?.length > 0),
        { timeout: 30000, interval: 2000 }
      );

      // 4. Fetch the message and follow the magic link
      cy.request({ url: "https://api.yobox.dev/mail/messages", headers: authHeaders }).then(
        ({ body }) => {
          const messageId = body.messages[0].id;
          cy.request({
            url: `https://api.yobox.dev/mail/messages/${messageId}`,
            headers: authHeaders,
          }).then(({ body: msg }) => {
            const link = msg.html.match(/https?:\/\/[^"']+/)[0];
            cy.visit(link);
            cy.contains("Welcome").should("be.visible");
          });
        }
      );
    });
  });
});
```

## Like this example?

⭐ Star the repository:
https://github.com/hocineman4/yobox-examples

🌐 More developer tools:
https://yobox.dev

## Links

- Tool: [YoBox Temp Mail](https://yobox.dev/?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
- Guide: [The Complete Cypress Guide](https://yobox.dev/blog/cypress-e2e-with-yobox-disposable-email-and-webhook-tester?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
