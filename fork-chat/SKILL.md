---
name: "fork-chat"
description: "Pull everything about one topic out of a past Claude chat into a handoff .md, so it can continue in a new chat or project. Use when the user says fork, extract, or pull out a topic from a chat."
---

# Fork-chat

Copies one topic out of a mixed chat into two .md files, like forking a repo: a full context file for the next AI, and a short summary for the human. The original chat stays as it is. The file is a summary, not the actual messages, so every point links back to where it came from.

Status: untested for accuracy. No evaluation has been done on how much it misses.

## Inputs
- **Source chat:** a link, a title, or "this chat". If it's a title, find it with conversation_search or recent_chats. Never guess a chat id.
- **Topic:** what to pull out. If the user didn't name one, ask in one line.

## Steps

1. **Check access.** Past-chat tools only see chats in the same scope: outside a project, only chats not in any project; inside a project, only that project's chats. If the chat can't be opened, tell the user to run this from where the chat lives (or before moving it), and stop.

2. **Find the topic.**
   - Run conversation_search with within_conversation_id for 3–5 different keyword sets: the topic name, its synonyms, names of files, skills, people or tools tied to it. One keyword is not enough.
   - For the best hits, open the chat at the hit's page_token with read_conversation. This gives turn numbers, which search results don't. Use next_page_token only where the topic is cut off at the page edge.
   - If searches return nothing (this happens), read the chat with read_conversation from the top, up to 50 turns per call. Pages can come back short when turns are long. Stop at 4 reads and say what was not read.
   - If a point was found by search but its turn number is unknown, say "later in chat" instead of guessing a number.
   - For "this chat", use read_conversation with conversation_id "current".

3. **Sort each relevant turn** into: decisions, things built (files, skills, repos, links), facts and numbers, the user's own instructions or preferences, open questions, and next steps. Record the turn number for each.

4. **Be strict about what counts.**
   - Include only what is about the topic. List what was left out in one line.
   - Keep who said what straight. Something Claude suggested is not a user decision unless the user agreed to it.
   - Do not add new advice or facts that are not in the chat. Gaps go under Open questions.

5. **Write the AI context file** as `fork-<topic>-<YYYY-MM-DD>.md`. This one is for the next Claude, so be complete: exact names, versions, file names, settings, numbers and the user's rules.



```
# Fork: <topic>
**Source chat:** [<title>](<url>) (turns X–Y of N)
**Forked:** <date>
**Topic asked for:** <topic>
**Left out:** <other topics in the chat, one line>

## The goal / idea
## Decisions (with turn numbers)
## Built so far (files, skills, repos, links)
## Key facts and numbers
## User's instructions and preferences
## Open questions
## Sources cited in the chat
## To continue
Paste into a new chat: "Continue from this fork. <one-line next step>"
```

Skip any section that would be empty. Bullets, plain words, no filler.

6. **Write the human summary** as `fork-<topic>-<YYYY-MM-DD>-summary.md`. Readable in under a minute (about 150 words max):

```
# What I pulled: <topic>
From **<chat title>** (<N> turns). Read time: under a minute.

**Got:** 3–6 short bullets
**Didn't get:** what was missing, unreadable, or not pinned to a turn, and where to find it
**Left out on purpose:** other topics, one line
**Check:** anything contradictory or worth verifying (skip if none)
```

The "Didn't get" part is the most important: be honest about gaps.

7. **Deliver** both files. In chat, say one line about each. Don't paste either file.

## Multiple topics
If the user asks to split a chat into several topics, make one pair of files per topic.

## Limits (say these if asked)
- It's a copy of context, not the messages. Claude can't move or split chats.
- Search can miss things phrased with words it didn't try. The turn links let the user check.
- Chats in another project can't be reached from here.
