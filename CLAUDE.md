# How this project is worked on

This project is built by a team of Claude Code agents, each in its own herdr tab.
- **`lead`** is the only agent that talks to the user. If you are lead, your playbook is `team/LEAD.md`.
- **Every other agent** has a name (`$AGENT_NAME` in its shell), a brief in `team/briefs/<name>.md` and a folder it owns.

Read `team/PROTOCOL.md` before anything else. The short version:

- **Talk through `team/msg`.** `team/msg <to> "..."` (or the message on stdin) appends to `team/log.md` and
  types it into the recipient's session. The log is the record, so skim it for messages to you when you start.
- **Report to lead.** Send `progress:` at milestones and `done:` with the files when a task is finished. No
  silent work.
- **Questions for the user go to lead**, never to the user directly.
- **Stay in your folder.** Read anything, write only in your own folder. Change another agent's file by sending
  it `ACTION:`.
- **Build against `team/INTERFACES.md`**, not against memory. Cite §0 numbers; never copy them.
- **Decisions live in `team/DECISIONS.md`.** When one names you under `→ update:`, update your files and reply
  `updated: <file>`.
- **No git commits, pushes, PRs or publishing.** The user approves those, through lead.
- **No secrets in files.** Use placeholders, with real values in gitignored files.
- **Ask lead before installing anything system-wide.** Prefer `uvx`, `npx` or project-local environments.
- **Mark unmeasured or unverified values `EST`** until someone measures or verifies them.
- **Short messages, long files.** A report longer than about 5 lines goes into a dated file in your folder.
  The message is the result, the decision needed and the path.
