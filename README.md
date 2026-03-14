# dev-squad 🤖

<!-- Add a banner image here: ![dev-squad banner](assets/banner.png) -->

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-blueviolet)](https://claude.ai)

`dev-squad` is a Claude Code plugin that assembles an AI engineering team to implement GitHub issues end-to-end and deliver a pull request.

When you run `/dev-squad <github-issue-url>`, it doesn't just start writing code. A Ticket Analyst reads the issue and produces an acceptance criteria document — which you review and approve before a single line of code is written. Then the right specialists are assembled: backend, frontend, database, DevOps, Playwright, documentation — running in the optimal order, some in parallel. A Code Simplifier strips over-engineering. A Code Reviewer audits the full changeset. Then a PR lands in your repo.

You stay in control through four checkpoints. The squad does the rest.


## Installation

### Claude Code

> **Marketplace listing coming soon. 🤞** In the meantime, see [Manual Installation](#manual-installation) below.

### Manual Installation

1. Clone this repo somewhere on your machine:
   ```bash
   git clone https://github.com/briannaworkman/dev-squad-plugin ~/dev-squad-plugin
   ```

2. Register the local marketplace and install:
   ```
   /plugin marketplace add ~/dev-squad-plugin
   /plugin install dev-squad@dev-squad
   ```

3. Verify by typing `/dev-squad` — it should autocomplete.


## Basic Workflow

<!-- Add a workflow diagram here: ![workflow diagram](assets/workflow.png) -->

1. 🟣 **Ticket Analysis** — A Ticket Analyst reads the GitHub issue and produces a structured plan: scope, acceptance criteria, and which agents are needed. You review and approve before any code is written. **(Checkpoint 1)**

2. ⚙️ **Implementation** — The right specialists assemble and execute in order. Database changes run before backend logic. Backend and frontend run in parallel when both are needed. DevOps, Playwright, and Documentation follow once the core is stable.

3. 🩵 **Simplification** — A Code Simplifier (via `pr-review-toolkit`) audits the full changeset and removes over-engineering.

4. 🔴 **Code Review** — A Code Reviewer does a full audit, reporting findings by severity. Critical issues block progress; the squad iterates up to 3 times before escalating to you. **(Checkpoint 2 & 3)**

5. 🚀 **Pull Request** — A PR is opened with a summary of the work. **(Checkpoint 4)**

The squad pauses for your approval at each checkpoint. Everything in between runs autonomously.


## Agent Roster

| Agent | Role |
|---|---|
| 🟣 **Ticket Analyst** | Always runs first. Reads the issue, defines scope, produces acceptance criteria, recommends which agents are needed. |
| 🟠 **Database Engineer** | Schema changes, migrations, query optimization. Runs before backend to avoid dependency issues. |
| 🔵 **Backend Dev** | APIs, business logic, server-side code. |
| 🩷 **Frontend Dev** | UI, client-side logic, styling. Runs in parallel with Backend when both are needed. |
| ⚫ **DevOps Engineer** | CI/CD, infrastructure, deployment config. Runs after core implementation. |
| 🟢 **Playwright Engineer** | End-to-end and acceptance test coverage. |
| 🟡 **Documentation Writer** | README updates, API docs, changelogs. Runs in parallel with Playwright. |
| 🩵 **Code Simplifier** | Removes over-engineering from the full changeset. Always runs before Code Reviewer. |
| 🔴 **Code Reviewer** | Always runs last. Full changeset audit with severity-rated findings. |

Not every agent runs on every issue — the Ticket Analyst recommends which agents are needed, and after you approve the plan, the orchestrator dispatches them automatically.


## Prerequisites

- 🔑 **GitHub CLI** authenticated: `gh auth login`
- 🔧 **[pr-review-toolkit](https://claude.ai/plugins/pr-review-toolkit)** plugin installed (provides Code Simplifier)
- 📦 **[commit-commands](https://claude.ai/plugins/commit-commands)** plugin installed (used by agents to commit and push)
- ⚡ **[superpowers](https://claude.ai/plugins/superpowers)** plugin installed (used by agents for TDD and planning workflows)


## Philosophy

- 🧑‍✈️ **Human checkpoints, not human bottlenecks** — You approve the plan before code is written, review the implementation before it's scrutinized, and sign off on findings before a PR opens. Everything in between runs autonomously.
- 🎯 **Right agent for the right job** — Specialists outperform generalists. Each agent has a focused role, the tools it needs, and nothing more.
- ✂️ **Simplicity enforced, not hoped for** — Code Simplifier runs on every changeset before review. Over-engineering doesn't survive the pipeline.
- 🚦 **Quality gates, not vibes** — Code Reviewer reports findings by severity. Critical issues block the PR. The squad iterates up to three times before escalating to you.


## Contributing

Agent definitions live in `agents/`. The slash command orchestrator is in `commands/dev-squad.md`.

To add or modify an agent:

1. Fork the repository
2. Edit or create the agent markdown file in `agents/`
3. Test end-to-end with a real GitHub issue
4. Submit a PR


## Updating

Pull the latest changes and reload:

```bash
cd ~/dev-squad-plugin && git pull
```

Then in Claude Code:

```
/reload-plugins
```

Once the plugin is available on the official marketplace, updates will be as simple as:

```
/plugin update dev-squad
```


## License

MIT License — see LICENSE file for details.


## Limitations

- **Single-repo only** — dev-squad works within the repository you run it from. Multi-repo setups (e.g. separate frontend/backend repos or microservices across different repositories) are not currently supported. A monorepo or a well-scoped single-service issue works best.
- **Public GitHub issues only** — the Ticket Analyst fetches issue content via the `gh` CLI, which requires the issue to be accessible with your authenticated GitHub account.
- **Well-scoped issues work best** — very large or ambiguous issues may be flagged by the Ticket Analyst as too broad for a single PR. Breaking them into smaller issues first will get better results.


## Support

- **Issues**: https://github.com/briannaworkman/dev-squad-plugin/issues
