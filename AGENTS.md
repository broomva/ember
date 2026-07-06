# AGENTS.md — Operational Rules

Operational companion to [`CLAUDE.md`](CLAUDE.md) (the invariants). This repo runs on the
[bstack](https://github.com/broomva/bstack) agent harness.

## Setup

```bash
npx skills add broomva/bstack   # install the harness (governance, hooks, primitives)
bun install                     # dependencies
```

## The work loop

1. **Snapshot before acting** — `git status`, branch, open PRs, CI state. Plans built on stale
   state fail silently.
2. **Ticket** — every significant unit of work is tracked. No significant work without one.
3. **Branch → PR → CI → merge** — never commit straight to `main`; never merge with failing checks.
4. **Dependency-chain reasoning** — before a substantive change, write the upstream + downstream
   file/function list in the PR body.
5. **Validate by interacting** — run the change (build, dev server, the affected flow) and capture
   evidence before claiming it works.
6. **Clean tree discipline** — a clean `git status` is the only reliable reset point; start each
   new unit of work from one.

## Gates (see `.control/policy.yaml`)

- **G1 — No secrets** committed. Use `.env` (gitignored); never paste keys into code or chat.
- **G2 — No destructive ops** (force-push to `main`, history rewrite, bulk delete) without explicit
  confirmation.
- **G3 — No merge on red** — CI must be green.
- **G4 — Governance present** — `CLAUDE.md`, `AGENTS.md`, `.control/policy.yaml` must exist.

## Conventions (enforced)

bun · Biome (not ESLint/Prettier) · Better Auth (not NextAuth) · Vercel · eve. TypeScript for web.
Agent behavior is data (`authored-agents-as-data`) — a prompt/tool change is a diff, not a code
rewrite.

## Architecture guardrails

- Don't adopt a runtime's proprietary primitives (memory/eval/consolidation/credentials) as
  product layers — keep them in our own store behind the `ExecutionHost` seam. **Own the mind,
  rent the body.**
- The per-user record lives in our own portable store. Never make it depend on a single vendor's
  durable primitive.
- No agent path may free-form self-modify a live workspace — evolution is always propose → test →
  approve → versioned diff.
