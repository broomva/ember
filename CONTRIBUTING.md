# Contributing to Ember

Thanks for your interest. Ember is early and design-first — the most useful contributions right now
are ideas, issues, and design/architecture feedback.

## Ground rules

- Read [`CLAUDE.md`](CLAUDE.md) (invariants) and [`AGENTS.md`](AGENTS.md) (operational rules) first.
- **Conventions are enforced:** bun (not npm/yarn) · Biome (not ESLint/Prettier) · Better Auth (not
  NextAuth) · TypeScript for web.
- **Branch → PR → CI → merge.** No direct commits to `main`; no merging with failing checks.
- **Small, surgical diffs.** In the PR body, note what the change depends on (upstream) and what
  depends on it (downstream).
- **No secrets** in code, commits, or chat. Use `.env` (gitignored).

## Getting started

```bash
git clone https://github.com/broomva/ember
cd ember
npx skills add broomva/bstack   # optional: the agent harness
bun install
```

The app scaffold (Next.js / bun / Biome / Better Auth) lands as it's built.

## Architecture guardrails

Ember's design has a few non-negotiables (see [`docs/architecture.md`](docs/architecture.md)):

- **Own the mind, rent the body** — the runtime is swappable behind the `ExecutionHost` seam; don't
  couple product logic to one runtime's proprietary primitives.
- **Own the record** — the per-user workspace lives in our own portable store.
- **Gated evolution** — agents never free-form self-modify a live workspace.

## License

By contributing, you agree your contributions are licensed under [Apache-2.0](LICENSE).
