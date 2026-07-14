# Regex Patterns for QA

Battle-tested regex snippets for the validation problems that show up in every QA suite.

## Workflow

Copy the pattern that matches your problem, drop it into your test suite, and validate it in the YoBox Regex Assistant against your real fixtures before shipping.

## Patterns

```js
// Email — practical, not RFC-perfect
/^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/

// International phone (E.164)
/^\+?[1-9]\d{6,14}$/

// UUID v4
/^[0-9a-f]{8}-[0-9a-f]{4}-4[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$/i

// ISO 8601 timestamp
/^\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}(\.\d+)?(Z|[+-]\d{2}:?\d{2})$/

// URL (http/https)
/^https?:\/\/[^\s/$.?#].[^\s]*$/i

// Semver
/^(\d+)\.(\d+)\.(\d+)(?:-([0-9A-Za-z.-]+))?(?:\+([0-9A-Za-z.-]+))?$/

// Slug
/^[a-z0-9]+(?:-[a-z0-9]+)*$/

// Hex color
/^#([0-9a-f]{3}|[0-9a-f]{6})$/i

// JWT
/^[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+$/

// Credit card (Luhn should validate the result)
/^\d{13,19}$/
```

## Like this example?

⭐ Star the repository:
https://github.com/hocineman4/yobox-examples

🌐 More developer tools:
https://yobox.dev

## Links

- Tool: [YoBox Regex Assistant](https://yobox.dev/tools/regex-assistant?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
- Guide: [10 Regex Patterns Every QA Engineer Should Memorize](https://yobox.dev/blog/regex-patterns-every-qa-engineer-should-memorize?utm_source=github&utm_medium=example&utm_campaign=yobox_growth)
