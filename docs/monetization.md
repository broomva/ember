# Ember — Open Core

Ember follows an **open-core** model, in the spirit of Supabase: the engine is fully open source,
and a managed cloud is the paid product. The open source is not a teaser — it is the whole engine,
self-hostable, with no lock-in. That openness is the point: it removes lock-in fear, earns trust,
and is the distribution engine.

## The principle: own your data, rent the convenience

This is the company-level version of Ember's core architectural principle — **own the mind, rent
the body**:

- **The mind is open.** The agent engine, the Forge, the tool-pack, and the surface are
  open-source and self-hostable on your own infrastructure and your own store. Your agents —
  and everything they learn about you — are portable git-versioned data you can export anytime.
- **The body is a service.** Running it well at scale (hosting, the multi-tenant control plane,
  managed storage and backups, reliability, support) is the convenience you can choose to pay for.

Your agent's accumulated, personalized workspace is never held hostage. The reason to stay is that
it keeps getting better and it just works — not that your data is locked in.

## What's open source (Apache-2.0)

- **The agent engine** — the recursive agent substrate (one primitive: forge / operator / evolver
  as configs), the shared tool-pack, the gated evolve loop.
- **The Forge** — absorb a problem or a file into a working, self-improving agent.
- **The surface** — the web/PWA app and the Broomva Design System.
- **Self-hosting** — run the whole thing on your own Vercel + your own store.

## Managed Ember Cloud (the paid product)

For people who want zero setup and don't want to operate infrastructure:

- **Hosted Forge-as-a-service** — create an agent from a conversation, no deploy step.
- **The multi-tenant control plane** — signup, provisioning, routing, per-tenant isolation.
- **Managed storage** — your workspaces hosted, backed up, and versioned for you.
- **Reliability + support** — uptime, updates, and help.
- **Cross-org improvements** — privacy-preserving learning that makes onboarding better over time.

## Tiers (philosophy, not a price sheet)

- **Free** — generous enough to run a real personal agent, so the product proves itself before you
  ever pay.
- **Pro** — more agents, more usage, voice.
- **Team** — shared agents, roles, collaboration.
- **Enterprise** — self-hosted support, SSO, data-residency and compliance options.

The dominant cost of onboarding a new agent is human setup labor, not compute — so the value
Managed Cloud sells is *the Forge doing that setup for you*, and keeping it running.

## Why open, not closed

- **No lock-in → faster adoption.** People try tools they can leave. Self-hostability is the
  strongest possible "you can leave" signal.
- **Distribution.** The open-source project is the top of the funnel — community, trust, and reach
  that a closed product has to buy.
- **The moat survives it.** Ember's durable advantage is the accumulated, personalized per-user
  agent (a switching cost that is *the user's own relationship-as-data*, uncopyable) plus the
  convenience of the managed service — not the source code. Open-sourcing the engine costs nothing
  the moat depends on.

## Trademarks

The Apache-2.0 license covers the code. "Ember," "Broomva," and associated logos are trademarks and
are not licensed for use in a way that implies affiliation or endorsement. You can self-host and
build on the code; please don't call your fork "Ember."
