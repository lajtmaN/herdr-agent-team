# Bootstrapped: a lead + agent team in herdr

A way of working for a team of Claude Code agents.
- **One lead** talks to you, splits the work, decides, reviews and reports.
- **Specialist agents**, each in its own herdr tab, own one folder each. They report to the lead and talk to each other through one shared log.

Nothing here is tied to a project. The project itself comes from the first prompt.

## Start a new project

1. Copy this folder's contents into the new project's root. Keep `CLAUDE.md` and `team/` at the root.
2. `chmod +x team/msg team/spawn team/unanswered team/await-reply`
3. Open the project in a herdr workspace. In the first pane, start Claude Code: `claude --permission-mode auto`.
4. Paste `INITIAL-PROMPT.md` and fill in the project goal at the top. The lead sets up the team from there.

## What's in it

| File | What |
|---|---|
| `INITIAL-PROMPT.md` | The prompt that starts the lead and its loop |
| `CLAUDE.md` | Rules every agent loads: roles, folders, no commits, how to talk |
| `team/LEAD.md` | The lead's playbook: the loop, delegation, reviews, reporting to the user |
| `team/PROTOCOL.md` | The team rules (messaging, contracts, decisions, reminders) and the roster |
| `team/DECISIONS.md` | Everything the user said, and every decision, with who must update what |
| `team/INTERFACES.md` | The contract between agents, plus §0 "Numbers": every headline number lives here once |
| `team/log.md` | Every message between agents: the permanent record |
| `team/briefs/` | One brief per agent. `_TEMPLATE.md` to start from, `coach.md` ready to use |
| `team/msg` | Send a message: it is appended to the log and typed into the recipient's session |
| `team/spawn` | Start an agent in a new herdr tab with its brief |
| `team/unanswered` | The lead's inbox: messages to lead it hasn't answered yet |
| `team/await-reply` | An agent waits for the lead's answer, then re-asks with `REMINDER:` |
| `team/roster` | Agent names, one per line (`team/spawn` adds them; `team/msg all` reads it) |

## Requirements

- herdr, with this session running inside it (`HERDR_ENV=1`, `HERDR_WORKSPACE_ID` set).
- Claude Code, and `python3` for the scripts.
- To start agents with another command, set `AGENT_CMD`, e.g. `AGENT_CMD="claude --model opus --permission-mode auto"`. If that command's prompt doesn't show "auto mode on", set `AGENT_READY` to a regex for its ready screen.
