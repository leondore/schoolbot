# Updates carry the full state; code derives the patch

Refines ADR 0007. An update Action carries the School event's complete new state (the same shape as a create), not a list of changed fields. Code compares it with the School event as we last wrote it in our store and patches only the fields that differ, so a Parent's hand edits in Google Calendar still survive on every field the school didn't change, and fields we never write are never touched. The model never reasons about "unchanged" fields, and update reuses create's shape, which matters under Anthropic's limit on union-typed properties in a structured-output schema.

## Consequences

A model that rewords an unchanged title or details produces a diff, and with it an overwrite of any hand edit to that field. Three guards: the prompt tells the model to copy unchanged fields verbatim, the evals assert that update cases keep the title unchanged, and the Proposal shows each changed field as old → new so a Parent can spot and deselect an unwanted overwrite.

## Considered Options

- **Patch Actions** (the model names only the fields that changed). Closer to what Calendar receives, but every field becomes optional or nullable twice over, blowing the union budget, and "unchanged" versus "cleared" becomes ambiguous.
