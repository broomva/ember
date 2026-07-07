# Ember — Agent Workspace Instructions

Ember is an open-source platform to **create, operate, and evolve personal agents**. This file is
the invariant context for any agent — human or AI — working in this repo. It is enforced by
reasoning, not just tooling.

## What Ember is

A hosted **Forge** turns a user's problem (or a file they already use) into a live agent in its own
workspace that keeps personalizing itself. One loop, over any domain: **create → operate → evolve**.
Full picture: [`docs/architecture.md`](docs/architecture.md).

## Architecture invariants

- **Five layers** — surface · control · substrate · runtime · record.
- **One recursive primitive** — the forge, operator, and evolver are configs of a single agent
  shape (`instructions · tools/ · skills/ · channels · gate · schemas`). Agent behavior is
  versioned *data*, not code. Tuning an agent is a diff, not a rewrite.
- **Own the mind, rent the body** — own the definition substrate, the tool-pack, the
  memory/evolution model, the surface, and the absorption engine. Rent the runtime (agent loop +
  sandbox + inference) behind the `ExecutionHost` seam. Never adopt a runtime's proprietary
  primitives as product layers.
- **Own the record** — the per-user workspace-as-data lives in our own portable, S3-compatible
  store, never a vendor-locked primitive. The runtime FUSE-mounts it for reads; write-back (gated
  diffs) commits through our own git/DB path.
- **Gated evolution** — no agent free-form self-modifies live. Propose a diff → test against frozen
  fixtures → surface at the gate → user approves → versioned, revertable commit.
- **The gate is the user's** — no loop auto-completes; "needs you" is a gate, not a failure.

## Conventions

- **Package manager:** bun (never npm/yarn).
- **Linter:** Biome (never ESLint/Prettier).
- **Auth:** Better Auth (never NextAuth).
- **Deploy:** Vercel. **Runtime:** eve.
- **Web:** TypeScript / Next.js (installable PWA). **Design:** the Broomva Design System —
  cool-blue, calm, glass-earned; plain voice, sentence case.

## Development principles

Four disciplines, each backed by a concrete behavior (not a slogan):

| Principle | The concrete behavior |
|---|---|
| **Think before coding** | Enumerate the dependency chain — upstream (what this depends on) + downstream (what depends on it), with file paths — before a substantive change. |
| **Simplicity first** | No code nobody asked for. The simplest thing that works well. |
| **Surgical changes** | Diffs touch only what they must. |
| **Goal-driven** | Validate by *interacting* (run it, see it), not by reasoning. Reasoning isn't validation. |

## The harness

This repo is governed by **bstack** — the Broomva Stack agent harness. Install:
`npx skills add broomva/bstack`. Operational rules are in [`AGENTS.md`](AGENTS.md); enforceable
gates in [`.control/policy.yaml`](.control/policy.yaml).

## Repo structure

```
ember/
├── docs/            architecture.md · monetization.md
├── CLAUDE.md        this file — invariants
├── AGENTS.md        operational rules
└── .control/        policy.yaml — gates
```

The app scaffold (Next.js/bun/Biome/Better Auth) lands under `app/` (or `apps/web/`) as it's built.

## Verification

Run `bun run build`, lint, and tests before opening a PR. Never merge with failing checks.
