# schoolbot

Turns the school's WhatsApp messages into calendar entries, saved media and reminders, which the parents review in Telegram.

## Language

### The school

**School event**:
Something happening at school on a given date, as announced by the school: an act, a dress-up day, an exam, a day off.
_Avoid_: event (unqualified), activity

**Parent task**:
Something the school asks parents to do, send or buy for a School event ("👉 Padres: vestimenta rosa").
_Avoid_: parent action

**Efemérides**:
The school's weekly flyer of commemorative dates; each date becomes its own School event.

**Child**:
One of the family's children at the school.
_Avoid_: kid, student, son, daughter

**Audience**:
The Children a School event concerns; everyone unless the school says otherwise.

**Chat**:
An allowlisted WhatsApp chat the school uses to communicate, concerning one or more Children.
_Avoid_: group (for WhatsApp)

**Message**:
A WhatsApp message from a Chat, with any attached media.
_Avoid_: message (for anything posted in Telegram)

**Batch**:
The Messages from one Chat that arrive close enough together to be understood as one unit.
_Avoid_: burst, chunk

**Follow-up**:
Something the school said it will send later ("se enviará un listado…"), held open until a later Message fulfils it.
_Avoid_: pending item, todo

### What schoolbot produces

**Action**:
One change the agent proposes from a Batch: create, update or cancel a School event, save a photo, save a file, or open or close a Follow-up.
_Avoid_: change, operation, result

**Auto-applied**:
Describes an Action the review policy lets through without a Parent's decision, such as saving a photo.

**Check**:
A deterministic rule run on every Action, such as the stated weekday matching the date.
_Avoid_: validation

**Warning**:
The ⚠️ mark a failed Check puts on an Action, which forces it into review.
_Avoid_: validation error

**Escalation**:
Re-running a Batch on the stronger model because the first answer failed a Check, was not confident enough, or follows a Correction.

**Calendar entry**:
The Google Calendar mirror of a School event.
_Avoid_: event (for the Google object), appointment

### Review

**Parent**:
A person allowed to decide Proposals in the Review group.
_Avoid_: user, reviewer, admin

**Review group**:
The Telegram group where Parents review Proposals and receive Reminders.
_Avoid_: group, Telegram chat

**Proposal**:
The Actions from one Batch that need review, presented together and decided by a single approval or rejection; Parents can deselect individual Actions before approving.
_Avoid_: request, approval

**Superseded**:
Describes an Action in an open Proposal that a later Batch has replaced; it moves to the new Proposal and leaves the old one.
_Avoid_: replaced, obsolete

**Correction**:
A Parent's reply to a Proposal that changes its content, producing a new Proposal in its place.
_Avoid_: edit, feedback

**Reminder**:
A notice to the parents ahead of a School event, derived from the event and its Parent tasks rather than proposed on its own.
_Avoid_: alert
