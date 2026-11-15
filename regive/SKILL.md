---
name: regive
description: "Use when the user types regive (e.g. 'regive 1: X', 'regive 1+2: X', 'regive 2 redo: X'): show an earlier answer again with a new idea added after it."
---

# regive

The user had another idea after sending a message and wants one reply that holds both: the old answer first, then the new part after it. They want to read or copy everything in one place instead of scrolling back.

## Commands

| Command | Meaning |
|---|---|
| `regive 1: X` | Old answer to the user's most recent message before this one, then X added after it |
| `regive 2: X` | Same, but for the message two back (skip the latest) |
| `regive 1+2: X` | Both old answers, oldest first, then X added after them |
| `regive N redo: X` | X changes the old answer: show the reworked answer with X built in |
| `regive N short: X` | Only the new part, no reprint (cheaper) |

N counts back through the user's own messages, not counting the regive message. 1 is the latest one.

### Example

The user sent "ideas for a landing page", then "best fonts for it".

- `regive 1: also dark mode` shows the fonts answer, then dark mode added after it.
- `regive 2: also dark mode` shows the landing page answer, then dark mode added after it.

## Default mode

1. Find the target message and your reply to it.
2. Reprint that reply exactly as it was: same words, headings, lists and formatting. Leave out any lines that only talked about files or tools (e.g. "here's the file"), since those don't repeat.
3. Add a divider line: `**Added: <X in a few words>**`
4. Answer X in the same format as the old reply. If the old reply was a numbered list ending at 5, start at 6. If it had sections, add a section that fits.
5. If X changes an old point, say so in one line in the new part ("this also changes point 3: ..."). Leave the reprinted part unchanged so it matches what the user saw before.

With `1+2`, reprint both replies, oldest first, then the divider and the new part fitted to both.

## Redo mode

X changes the old answer. Show the whole answer again with X worked in: changed parts rewritten in place, new points where they fit. End with one line naming what changed ("Changed: points 2 and 4. Added: point 6.").

## Short mode

Only the new part: start with `Add-on to the answer for "<first few words of that message>"`, then answer X in the old reply's format. Do not reprint or summarize the old answer.

## Edge cases

- If you never replied to the target message, answer it and X together as one reply.
- If N is beyond the start of the chat, or it's unclear which message is meant, ask in one line.
- `regive` with no number means `regive 1`.
