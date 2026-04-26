# AI Factory Template

A **provider-agnostic** multi-agent AI software team. 6 markdown agent prompts (PO + Frontend, Backend, DevOps, QA, Security) backed by a project wiki. Works with **any AI coding tool**.

Inspired by [Karpathy's LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

## What You Get

```
agents/                     # Agent prompts (plain markdown — copy into any tool)
├── po.md                   # Product Owner / Orchestrator
├── frontend.md             # Senior Frontend Engineer
├── backend.md              # Senior Backend Engineer
├── devops.md               # Senior DevOps/SRE Engineer
├── qa.md                   # Senior QA Engineer
└── security.md             # Senior Security Engineer

wiki/                       # Project wiki (knowledge base)
├── SCHEMA.md               # Schema — how agents use the wiki
├── templates/              # Page templates (ADR, sprint, runbook, incident, etc.)
└── wiki/                   # Agent-maintained pages
    ├── project.md          # Tech stack, conventions, environments
    ├── index.md            # Master page index
    ├── log.md              # Activity timeline
    ├── docs/               # ADRs, API docs, guides
    ├── architecture/       # System diagrams, service maps
    ├── runbooks/           # Operational procedures
    ├── sprints/            # Sprint tracking
    └── projects/           # Sub-projects, features
```

## Agent Team

| Agent | File | Handles |
|-------|------|---------|
| Product Owner | `po.md` | Task breakdown, delegation, code review, integration |
| Frontend | `frontend.md` | React/Next.js, TypeScript, UI/UX, accessibility |
| Backend | `backend.md` | APIs, databases, auth, business logic |
| DevOps | `devops.md` | CI/CD, Terraform, Kubernetes, monitoring |
| QA | `qa.md` | Test strategy, E2E automation, performance testing |
| Security | `security.md` | Threat modeling, OWASP, secure code review |

## Setup by Provider

### Claude Code (Anthropic)

```bash
# Copy PO prompt as system prompt
cp agents/po.md .claude/system-prompt.md

# Or use CLAUDE.md convention
cp agents/po.md CLAUDE.md
```

Switch roles by pasting agent prompts:
```
/read agents/frontend.md
Now act as the Frontend Engineer and build a login form.
```

### Cursor

Add to `.cursor/rules`:
```
Read agents/po.md for your role.
Read wiki/wiki/project.md for project context.
Read wiki/SCHEMA.md for wiki rules.
```

Or paste individual agent prompts into Cursor's system prompt settings.

### Aider

```bash
# Use PO as main prompt
aider --read agents/po.md

# Add project context
aider --read agents/po.md --read wiki/wiki/project.md
```

### OpenCode / Kiro CLI

```bash
# These support agent configs natively — see kiro-factory-template
# for the Kiro CLI-specific version with JSON configs and hooks
```

### ChatGPT / Any Chat UI

1. Start a conversation
2. Paste the content of `agents/po.md` as your first message
3. Then describe your task
4. When you need a specific role, paste that agent's prompt

### Any Tool with System Prompts

The `agents/*.md` files are plain markdown. Copy their content into whatever "system prompt", "custom instructions", or "rules" field your tool provides.

## Quick Start

```bash
git clone https://github.com/fonthap/ai-factory-template.git
cd ai-factory-template

# 1. Edit wiki/wiki/project.md — add your tech stack and conventions
# 2. Load agents/po.md into your AI tool
# 3. Start building
```

### Example prompts

```
"build a login page with email/password form"
"add a REST API for user CRUD with PostgreSQL"
"set up GitHub Actions CI pipeline with lint, test, build"
"write E2E tests for the checkout flow"
"review this PR for security issues"
```

## How It Works

1. You describe a feature or task
2. The PO agent reads `wiki/project.md` for context
3. It plans which roles are needed (frontend, backend, etc.)
4. Each role produces code, tests, infra, or docs
5. Results are reviewed and integrated
6. Wiki is updated — knowledge compounds over time

## Customization

### Add/remove agents
Create a new `agents/<role>.md` with the same structure (Expertise, Rules, Output Structure, Self-Check). Add it to the team table in `agents/po.md`.

### Change the wiki structure
Edit `wiki/SCHEMA.md` to change sections, naming conventions, or workflows.

### Add templates
Drop new templates in `wiki/templates/` — agents will use them when creating wiki pages.

## vs. Kiro Factory Template

| | AI Factory (this repo) | [Kiro Factory](https://github.com/fonthap/kiro-factory-template) |
|---|---|---|
| Provider | Any AI tool | Kiro CLI only |
| Agent format | Plain markdown | JSON configs |
| Multi-agent | Manual (paste prompts) | Native DAG delegation |
| Hooks | None | Logging, cost tracking, traces |
| Skills | None | Kiro CLI skills system |
| Best for | Quick start, any tool | Full automation, Kiro CLI users |

## License

MIT
