# Batch-level Proposals with stored Action status

A Proposal holds every reviewable Action from one Batch in a single Telegram message, decided by one submit (*Aprobar selección* or *Rechazar todo*). Each Action's status (selected, deselected, superseded) lives in our store, not in the Workflow. Toggles and supersession only update that status and redraw the message; the Workflow waits for the submit alone and, on approval, applies whichever Actions are selected at that moment.

This keeps one wait per Workflow, so a forgotten item can't leave it hanging, while still letting Parents drop single items without a Correction, and lets a later Batch supersede one Action out of an open Proposal without signalling its Workflow. Status writes are conditional, so a submit and a supersession racing on the same Action resolve to exactly one School event. When every Action in a Proposal is superseded, the Proposal closes as replaced.

## Considered Options

- **One Telegram message per Action.** Friendlier for picking items, but a weekly Efemérides flyer becomes a stream of messages and the Workflow waits on many events, any of which can be forgotten.
- **One message per Batch, all-or-nothing.** Simple, but dropping one item requires a Correction and another model call.
