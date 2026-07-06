# Ember

**Create, operate, and evolve your own personal agents.**

Ember turns a problem you describe — or a file you already use — into a live agent that lives in
its own workspace and **keeps personalizing itself** as you work with it. You talk to it, watch
it work, and approve or edit what it produces. It gets more *yours* every week.

Open-source engine. Managed cloud when you want zero setup.

> Status: **early / design-first.** This repo currently holds the architecture, the design
> system, and interactive PWA prototypes. The app scaffold is in progress — see
> [`docs/architecture.md`](docs/architecture.md).

## The loop

One loop, over any domain:

- **① Create** — describe a task, or drop a file you already use (a template, a transcript). A
  hosted **Forge** absorbs it and builds an agent. Creation is a conversation, never a form.
- **② Operate** — give it work; it runs; it pauses at **the gate** ("needs you"); you approve or
  edit; it files the result, with a receipt.
- **③ Evolve** — every edit teaches it. It proposes changes to *itself* — gated by your approval,
  with provenance — and becomes more yours over time. The workspace-as-data is the point.

## Architecture in one breath

Five layers — **surface** (this PWA) · **control plane** · the **Forge** (create + evolve) ·
**runtime** (eve on Vercel, behind a swappable `ExecutionHost` seam) · **substrate** (your
git-versioned workspaces + your own store — *the record is yours*). One **recursive primitive**:
the forge, the operator, and the evolver are all configs of the same agent shape. Full detail in
[`docs/architecture.md`](docs/architecture.md).

**Own the mind, rent the body.** The engine, the tool-pack, the memory/evolution model, and the
surface are yours and portable; the runtime (agent loop + sandbox + inference) is commodity muscle
behind a seam. Your agent's accumulated, personalized workspace is never locked to any vendor.

## Open core

The **engine is open source** (Apache-2.0) — self-host it on your own Vercel + your own store,
with no lock-in. **Managed Ember Cloud** gives you zero-setup hosting, the multi-tenant control
plane, managed storage + backups, and support. Own your data; rent the convenience. See
[`docs/monetization.md`](docs/monetization.md).

## What's in this repo

| Path | What |
|---|---|
| [`docs/architecture.md`](docs/architecture.md) | The technical architecture (layers, the Forge, the evolve loop, the surface, the data model, voice) |
| [`docs/monetization.md`](docs/monetization.md) | The open-core model (self-host vs Managed Cloud) |
| [`design-system/`](design-system/) | The Broomva Design System — tokens, components, and the work/gate/receipt vocabulary |
| [`prototypes/`](prototypes/) | Interactive PWA mockups — open the `.html` files in a browser |

## Built with

**bun** · **Biome** · **Better Auth** · Next.js (installable PWA) · **eve** on Vercel · AI Gateway.

## Agent-governed

This repo runs on the [**bstack**](https://github.com/broomva/bstack) agent harness (governance,
hooks, primitives). Install with `npx skills add broomva/bstack`; see [`CLAUDE.md`](CLAUDE.md) and
[`AGENTS.md`](AGENTS.md).

## License

[Apache-2.0](LICENSE) © 2026 Broomva.
