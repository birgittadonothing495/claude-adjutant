# Adjutant

An autonomous AI executive assistant. Zero code. Just markdown + Claude Code.

Adjutant runs 24/7 on your hardware, manages your projects, runs growth
experiments, handles email and calendar, and messages you proactively when
something needs your attention. It thinks strategically, delegates execution
to sub-agents, and gets smarter over time.

## How It Works

```
You (Telegram / Slack / Dispatch)
  ↓
Adjutant (Opus, always-on, always responsive)
  ├── Thinks: strategy, priorities, decisions
  ├── Delegates: execution to sub-agents (Sonnet/Haiku)
  └── Never: does manual work itself
        ↓
Knowledge System (markdown files)
  ├── SOUL.md        — personality, values, boundaries
  ├── heartbeat.md   — what to check every 30 minutes
  ├── queue.md       — single coordination point for all work
  ├── knowledge/     — people, projects, goals, decisions
  ├── skills/        — reusable workflows (growth loops, reviews, briefings)
  └── experiments/   — running and completed experiment tracking
```

## What Makes It Different

- **Zero code.** The entire system is markdown files + Claude Code configuration.
  No frameworks, no databases, no custom code.
- **SOUL.md.** A persistent identity document that evolves over time. Not just
  instructions — personality, values, and learned patterns.
- **Heartbeat.** A configurable checklist that runs every 30 minutes, making the
  agent proactive instead of reactive.
- **Queue.** A single markdown file that coordinates all work — sub-agents,
  experiments, scheduled jobs all write to one place.
- **Three-tier memory.** Hot (queue, ≤50 lines), warm (knowledge, loaded on
  demand), cold (archive, searchable). Context never bloats.

## Quick Start

1. Clone this repo to your machine
2. Edit SOUL.md with your personality and boundaries
3. Add your projects to knowledge/projects/
4. Install [Claude Code](https://code.claude.com/docs/en/quickstart)
5. Run: `cd adjutant && claude`

For 24/7 deployment on a headless Mac Mini, see [docs/SETUP.md](docs/SETUP.md).

## Architecture

See [docs/architecture.md](docs/architecture.md) for the full design, including
model routing, memory tiers, and the dispatch protocol.

## Requirements

- Claude Code with a Max or Pro subscription
- macOS (launchd) or Linux (systemd) for scheduling
- Optional: Google Workspace CLI (`gws`) for email/calendar
- Optional: Telegram bot for mobile interface

## License

MIT
