# A Durable Object per Chat, a Workflow per Batch

Each Chat has one Durable Object that resets a short alarm on every new Message, so a burst of photos becomes one Batch without races. When the alarm fires it starts one Workflow with a stable ID (`batch-<chat>-<seq>`) that owns the Batch's whole lifecycle: understand, Check, auto-apply, propose, wait for the Parents, act. Workflows checkpoint each step, retry steps individually, and cost nothing while waiting days for a tap, which is what a human-in-the-loop pipeline needs.
