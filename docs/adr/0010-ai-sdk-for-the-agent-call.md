# AI SDK for the agent call, pinned to native structured outputs

`runAgent` calls Claude through the Vercel AI SDK (`ai` + `@ai-sdk/anthropic`, `generateText` with `Output.object`) rather than `@anthropic-ai/sdk`. The Anthropic SDK's Zod helper moves `const` and `enum` into description text, so the API wouldn't enforce the Action type tags or the Parent task categories; the AI SDK keeps them, along with `anyOf`, and handles the rest of the conversion to Anthropic's strict subset. It also gives typed errors for schema mismatch, truncation and refusal, and a mock model that lets us unit-test the Escalation policy without a fake client.

## Consequences

- The structured-output mode is pinned to `outputFormat`, never `auto` or `jsonTool`: a change to the SDK's model catalogue must not quietly switch us to a forced tool call, which Sonnet 5.5 rejects (ADR 0003).
- The SDK rewrites settings it believes a model can't take, so thinking is configured explicitly per model and a smoke test asserts the request body carries what we asked for.
- The SDK doesn't check Anthropic's schema limits (24 optional, 16 union-typed properties). A test captures the request through a custom `fetch` and checks the schema the SDK actually sends.
- `pattern` isn't enforced by the API (the SDK moves it into the description). Times and references are validated by Zod and the Checks afterwards, so a bad value leads to Escalation rather than a silent error. Dates use `format: date`, which is enforced.

## Considered Options

- **`@anthropic-ai/sdk` with a hand-converted schema** sent with `transform: false`. Full control of the request body, but we'd own a converter to the strict subset, error mapping and a hand-written fake client.
