# Effect not adopted

We don't use Effect, not even partially. Cloudflare Workflows already provide the error handling that matters most here (durable retries with backoff, per-step timeouts, resuming after failure), and Effect's retry and scheduling layer would multiply with step retries rather than replace them. Most failures in this domain are ordinary outcomes (a failed Check, low confidence, Escalation) that plain discriminated unions model well. Runtime safety comes from Zod at every trust boundary (ingest payload, Telegram updates, Claude output, the Google fields we read, config) and strict TypeScript. Errors are classified at each Workflow step boundary: transient errors are thrown so Workflows retry them, permanent ones are thrown as `NonRetryableError`, and domain outcomes are returned as values, never thrown.

## Considered Options

- **Effect throughout.** No Workers or Workflows platform package, and nothing documents Effect inside `step.do` or a Durable Object alarm. The I/O modules (`effect/http`, `effect/sql`, `effect/ai`) are `@stability unstable`, and Drizzle's Effect integration exists only in a 1.0 release candidate.
- **Effect only in the agent module.** Two idioms and a `runPromise` bridge at every boundary, for typed errors in a small module. Effect also turns optional schema fields into nullable unions, which count against Anthropic's limit on union parameters.

v4 was weeks old at the time, and most examples and model training data are v3, which hurts agent-written code. Revisit if Effect ships a Cloudflare Workers or Workflows platform package, or if its I/O modules become stable.
