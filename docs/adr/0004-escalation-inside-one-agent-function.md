# Escalation inside one agent function

Claude Haiku 5.5 handles every Batch; the agent escalates to Sonnet 5.5 when Haiku's answer fails a Check, falls below the confidence threshold, or follows a Correction. Model names are configuration. The whole policy (call, decode, Check, maybe escalate) lives in a single `runAgent(input, deps)` in `worker/src/agent/`, which the Workflow runs as one step and the eval script calls unchanged, so evals exercise exactly what production runs. Context (upcoming School events, open Follow-ups, open Proposals) is loaded in an earlier step and passed in.

## Consequences

A Workflow retry after a failed Sonnet call repeats the Haiku call too. At about $0.001 per call that's cheaper than splitting the policy between the Workflow and the eval script.
