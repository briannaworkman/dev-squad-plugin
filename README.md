# tech-lead

AI engineering team orchestrator for Claude Code.

## Usage

```
/tech-lead <github-issue-url>
```

Reads the GitHub issue, breaks it into tasks, assigns work to specialized agents, and delivers a GitHub PR.

## Prerequisites

- `pr-review-toolkit` plugin must be installed (for Code Simplifier)
- `commit-commands` plugin must be installed (used by implementation agents to commit)
- `superpowers` plugin must be installed (used by implementation agents for TDD and planning workflows)
- GitHub CLI must be authenticated: `gh auth status`

## Agent Roster

| Agent | Color | Role |
|---|---|---|
| Ticket Analyst | Purple | Reads issue, produces acceptance criteria |
| Backend Dev | Blue | APIs, business logic, server-side code |
| Frontend Dev | Pink | UI, client-side logic, styling |
| Database Engineer | Orange | Schema, migrations, queries |
| DevOps Engineer | Gray | CI/CD, infra, deployment config |
| Playwright Engineer | Green | End-to-end test coverage |
| Documentation Writer | Yellow/Gold | README, API docs, changelogs |
| Code Reviewer | Red | Full changeset audit |
| Code Simplifier | Teal | (via pr-review-toolkit) Removes over-engineering |

## Checkpoints

The tech lead pauses for your approval at:
1. Plan — before writing any code
2. Implementation — before code review
3. Review findings — before opening PR
4. Done — PR URL
