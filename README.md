# loop-engineer-template

A starter template for building **loop engineers**: agents that get triggered on their own,
pick up work, ship it, verify it, and log what they learned, so the work compounds without you
prompting every step. It's the productized version of the setup my team runs in production, and
what I teach at [AI Builder Club](https://www.aibuilderclub.com/lp/loop-engineer?utm_source=github&utm_campaign=loop-engineer-template).

## What's a loop engineer?

The shift: you stop prompting a coding agent task-by-task, and start **designing loops**.

A loop is an agent that wakes up on a trigger (a cron, a webhook, an incident, another agent),
does some investigation and work, and writes what it found and did into a shared, file-based
memory. Next run it reads that memory and keeps going. The real power is **compounding**: many
loops (support, SEO, product, ads) read and write the *same* folders, so a friction the support
loop logs can get picked up by the product loop, and a keyword the ads loop finds can feed the
SEO loop. One shared brain, many loops.

Building one comes down to four ingredients:

1. **Triggers:** cron, webhook, an incident, or another agent wakes the loop at the right time.
2. **A file + logging structure:** the shared memory loops read and write (this template).
3. **Tools & connectors:** so the agent can do real work (your skills/MCPs).
4. **A codebase harness:** so the agent can run, test, and verify its own work autonomously.

This repo gives you #2 and #4 out of the box, plus the scaffolding to add the rest.

Want the full walkthrough of the concept and how my team designs compounding loops? Watch the video:

[![The loop engineer: how to design compounding agent loops](assets/video-thumbnail.png)](https://youtu.be/W6x-hb44C0c)

## What's included

```
loop-engineer-template/
├── ARCHITECTURE.md          the knowledge-base model (read this once)
├── CLAUDE.md                template for YOUR context: fill in the {{PLACEHOLDER}}s
├── LOG.md                   global work log (one line per bulk of work)
├── signals/  docs/  domains/  starter artifact + loop folders, each README IS its schema
└── .claude/
    ├── skills/
    │   ├── new-loop/                 spin up a new loop (domain): scaffold, test-run, write its contract
    │   ├── setup-codebase-harness/   the codebase harness: make any repo agent-ready
    │   ├── dev-local-setup/            └ one-command dev stack
    │   ├── e2e-setup/                  └ a real e2e test gate
    │   └── pr/                         └ verify-before-ship (a fresh sub-agent proves it works, then opens the PR)
    └── workflows/
        └── ship-change.js           ship a scoped code change end-to-end (worktree → implement → review → verify → PR)
```

- **The knowledge base** (`ARCHITECTURE.md`, `signals/ docs/ domains/`, `LOG.md`) is the shared
  memory: artifacts filed by kind, domains as loops, every file with an append-only `## Timeline`.
- **The codebase harness** (the skills under `.claude/skills/`) is what makes a code repo
  *legible, executable, and verifiable* so loops can ship code without you babysitting them.

## Quickstart

1. **Copy this folder** to wherever you want your agent's knowledge base to live.
2. **Fill in `CLAUDE.md`:** replace every `{{PLACEHOLDER}}`. This is the context the agent reads
   on every session, so it's the most important step.
3. **Read `ARCHITECTURE.md`** so you and the agent share the same model. It's short.
4. **Spin up your first loop.** In Claude Code: run `/new-loop`, then tell it the loop's name,
   goal, and what it should do. It scaffolds `domains/<loop>/README.md`, does one real test run,
   and logs it.
5. **Harness the repo your loop ships into.** Run `/setup-codebase-harness` in that code repo so
   the agent can run, test, and verify its own work.
6. **Let it run.** Each session the agent reads `CLAUDE.md` + the relevant domain README, does
   work, writes artifacts, and appends to `LOG.md`. For code changes it drives `ship-change.js`
   and ships via `/pr`.

## Requirements

- [Claude Code](https://claude.com/claude-code) (the skills + workflow assume it).
- `git`. That's the only hard dependency.
- `ship-change.js` and the harness skills want the repo they ship into to be a git repo with a
  working build/test setup. They use Codex for review if available, and degrade gracefully if not.

## Go deeper

This template gets you the structure. If you want to learn how to actually build agents and run
compounding loops for your own business, that's what I go deep on inside
**[AI Builder Club](https://www.aibuilderclub.com/lp/loop-engineer?utm_source=github&utm_campaign=loop-engineer-template)**:
weekly live builder workshops, courses on production AI agents, AI coding beyond the basics, and
building your first LLM apps, plus a community of people building the same way.

[![Join AI Builder Club](assets/ai-builder-club.png)](https://www.aibuilderclub.com/lp/loop-engineer?utm_source=github&utm_campaign=loop-engineer-template)

**→ [Join AI Builder Club](https://www.aibuilderclub.com/lp/loop-engineer?utm_source=github&utm_campaign=loop-engineer-template)**

Built by [Jason Zhou](https://x.com/jasonzhou1993) (AI Jason).
