# Team protocol

Every agent runs in its own herdr tab in this workspace. The user talks only to **lead**. Everyone else talks to
lead and to each other.

## Roster

| Name | Owns | Folder |
|------|------|--------|
| `lead` | Overall design, interfaces, decisions, user contact | `team/` |
| `coach` | How the team works: audits communication, suggests process changes | `coach/` |
| … | (lead adds a row per agent it spawns) | |

## Messaging

```sh
team/msg <to> "<message>"        # <to>: an agent name from team/roster, lead, or all
team/msg <to> < file.txt         # long or quote-heavy messages: on stdin
```

- `team/msg` appends the message to `team/log.md`, the permanent record. Then it types it into the recipient's session.
- If delivery fails, the message is still in the log.
- Lead reads its messages from the log through a watcher, so nothing is typed into lead's session.
- Every shell has `AGENT_NAME` set by `team/spawn`.

## Rules

1. **Report to lead.**
   - Send `progress: …` when you finish a milestone.
   - Send `done: …` when a task is finished, with the files you produced.
   - No silent work.
2. **Questions for the user go to lead,** never directly to the user. Lead answers or asks the user. The answers land in
   `team/DECISIONS.md`.
3. **Contracts.** `team/INTERFACES.md` is the contract between agents.
   - The **owner of a row edits it.** Say so in the log and tell the agents it affects.
   - Lead reviews the diff and posts `reviewed: §…`. No objection from lead within 30 min means accepted.
   - Headline numbers (costs, sizes, limits, test counts…) live once, in §0, with an owner per row. Other docs
     **cite** them ("≈ 42 ms, see INTERFACES §0") instead of copying them.
   - Don't build against a value you changed on your own.
4. **Stay in your folder.**
   - Read anything; write only in your own folder, plus `team/log.md` through `team/msg`.
   - Lead may grant an exception (e.g. a shared top-level doc with one owner). The exception goes in the roster.
5. **No git commits, pushes, PRs or publishing.** The user approves them, through lead.
6. **No secrets in files.** Use placeholders; the real values come from gitignored files.
7. **Sub-agents.** You may spawn your own sub-agents (the Agent tool) for parallel work inside your folder.
8. **Installing tools.** Install without global changes when you can (`uvx`, `npx`, project-local environments). Ask lead before installing
   anything system-wide.
9. **Never wait silently on lead.**
   - A message that needs an answer starts with `QUESTION:`, or `BLOCKED:` if you can't continue without it.
   - Right after sending it, run `team/await-reply <you> 10` in the background.
   - If it exits with NO REPLY, re-send the same question starting with `REMINDER:` and wait again.
   - Keep working on anything that isn't blocked.
10. **Decisions reach every copy.**
    - Every DECISIONS entry ends with `→ update: <file> (<owner>), …`.
    - Lead sends the decision to every owner listed. Each owner replies `updated: <file>` when done.
    - A reversal or a caveat goes to the same recipients as the original.
    - Before you report done, grep for the old value.
11. **Facts before building.** When the work depends on the real world (measurements, existing systems, user data,
    prices), send lead the few make-or-break questions as one batch for the user before you build on guesses.
    Mark any unverified value `EST` in docs and models until it's verified.
12. **Prefixes.**
    - `QUESTION:` and `BLOCKED:` (rule 9) need an answer.
    - `DECIDE:` asks lead for a decision, with options and your recommendation.
    - `ACTION:` asks another agent to change something it owns.
    - `progress:`, `done:`, `updated:` and `reviewed:` are reports.
13. **Short messages, long files.**
    - A report longer than about 5 lines goes into a dated file in your folder, e.g. `<folder>/reports/2026-01-31-topic.md`.
    - The message is at most 5 lines: the result, the decision needed (if any), and the path.
14. **Independent review.** Reviewers read the work cold, without the author's reasoning, and file their findings in
    their own folder. The author answers each finding (fixed, or why not) in a dated file. Lead decides any disputes.
