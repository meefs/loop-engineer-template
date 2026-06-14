# loop-engineer-setup

A starter kit for running **long-lived, autonomous agent loops** on top of a plain
**markdown-in-git** knowledge base. It's the generic, productized version of a setup that's
been driving real growth/ops work for [superdesign.dev](https://superdesign.dev).

The idea: your repo *is* the agent's brain and its work queue. Everything an agent learns,
decides, or ships is a small markdown file with frontmatter — diffable, reviewable, and
writable by the agent itself. No database to stand up, no app to deploy. Just `git`.

## What you get

| File | What it is |
|---|---|
| `ARCHITECTURE.md` | The knowledge-base model: artifacts-by-kind, domains-as-loops, the two-layer body, the rules. Read this once. |
| `CLAUDE.md` | A placeholder template for *your* context — who the agent is, what it works on, your tools. Fill it in. |
| `LOG.md` | The global activity feed (empty, with the entry grammar at the top). |
| `signals/ docs/ domains/` | The starter folders. Each has a `README` that **is** its schema. |
| `.claude/skills/new-loop/` | A skill that spins up a new loop (domain), test-runs it, and writes its README. |
| `.claude/workflows/ship-change.js` | A reusable workflow that ships a scoped code change end-to-end (worktree → implement → simplify → review → verify → PR). For loops that touch code. |

## Quickstart

1. **Copy this folder** to wherever you want your agent's knowledge base to live, and
   `git init` it (or fork/clone this repo).
2. **Fill in `CLAUDE.md`** — replace every `{{PLACEHOLDER}}`. This is the single most
   important step: it's the context the agent reads on every session.
3. **Read `ARCHITECTURE.md`** so you (and the agent) share the same model. It's short.
4. **Spin up your first loop.** In Claude Code, run the `new-loop` skill:
   > `/new-loop` — then tell it the loop's name, goal, and what it should do.

   It scaffolds `domains/<loop>/README.md`, does one real test run, and records the run in
   the loop's `## Timeline` and in `LOG.md`.
5. **Let it run.** Each session, the agent reads `CLAUDE.md` + the relevant domain README,
   does work, writes artifacts (`signals/ docs/ tasks/`), and appends to `LOG.md`. For code
   changes, it can drive `ship-change.js`.

## Core concepts (one paragraph)

An **artifact** is one markdown file with one job, filed by **kind**. Start with just two:
`signal` = evidence, `doc` = durable knowledge. Committed work lives as a backlog line in the
loop's README until it earns its own `task` kind. A **domain** is a **loop**: a thread of work
with a charter, a cadence, and metrics. Its
`README` holds the loop's live state and *links* to its artifacts (it never contains them).
Everything carries an optional append-only `## Timeline` — *body = what's true now, Timeline
= what happened*. The global `LOG.md` is the one-line-per-ship feed across all loops.

That's the whole system. Read `ARCHITECTURE.md` for the why and the rejected alternatives.

## Requirements

- [Claude Code](https://claude.com/claude-code) (the skills + workflow assume it).
- `git`. That's the only hard dependency.
- `ship-change.js` additionally wants the repo it ships into to be a git repo with a working
  build/test setup. It uses Codex for review if available and degrades to a plain review
  agent if not.
