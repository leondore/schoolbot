# One-shot agent with structured outputs

The agent makes one Claude call per Batch, with no tools and no agentic loop: Messages, images and PDFs go in together with context, and Actions come back as JSON constrained by a schema in `output_config.format`. The schema is the agent's whole interface, which is also the main defence against instructions hidden in flyers; Calendar changes still need a Parent's approval.

## Considered Options

- **Forced tool call** (`tool_choice` of `tool` or `any`) to get structured JSON. Tried in an earlier version and dropped: Sonnet 5.5 rejects it, which would break Escalation.
- **Agent with tools** (look up events, write to Calendar). Rejected: more injection surface and nondeterminism for no gain, since all the context it needs fits in one prompt.
