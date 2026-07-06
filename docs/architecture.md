# Ember — Architecture

Ember is a platform to **create, operate, and evolve personal agents**. A hosted **Forge** turns
any user's problem into a live agent that lives in its own git-versioned workspace and keeps
personalizing itself. The product is one loop over any domain: **create → operate → evolve**.

The governing principle is **own the mind, rent the body**: the parts that make Ember an app —
the definition substrate, the tool-pack, the memory/evolution model, the surface, and the
absorption engine — are owned and portable. The runtime (agent loop + tool sandbox + inference)
is commodity muscle, rented behind a swappable seam.

## The five layers

```
 L0  SURFACE      — the web/PWA app on the Broomva Design System
                    create mode (talk to the Forge) · operate mode (sessions · the gate · receipts)
 L1  CONTROL      — signup · workspace provisioning · operator→agent routing · runtime CRUD · metering
 L2  SUBSTRATE    — one agent primitive + a shared tool-pack; the Forge is an agent on it (recursion)
 L3  RUNTIME      — eve on Vercel, behind an ExecutionHost seam (alternate backends are swappable)
 L4  RECORD       — git-versioned workspaces + your own store (the moat) · event log · artifacts
```

| Layer | What it is | Owns vs rents |
|---|---|---|
| **L0 Surface** | web/PWA (Next.js · bun · Biome · Better Auth) on the Broomva Design System | owns the surface + the work/gate/receipt vocabulary |
| **L1 Control plane** | signup · provisioning · routing · runtime CRUD · metering | owns the tenant registry, event log, routing |
| **L2 Agent substrate** | one primitive + shared tool-pack; the Forge is an agent on it | owns the primitive, tool-pack, and portable governance |
| **L3 Runtime** | durable sessions, HITL, channels — **eve on Vercel**, behind the `ExecutionHost` seam | rents commodity compute; swappable |
| **L4 Record** | per-user workspaces (git) + your own object store; event log | **owns the record — the moat lives here** |

## One primitive, applied to itself

There is a single agent shape — a workspace directory: `instructions · tools/ · skills/ ·
channels · gate · schemas` (**authored-agents-as-data**). Everything Ember runs is a config of it:

- **Operator** — the primitive with a domain tool-set, a cheap model, a tight gate.
- **Forge** — the primitive whose tools *scaffold and deploy the primitive* — an agent that emits
  agents. Recursion made literal.
- **Evolver** — the primitive that *reads another agent's workspace + edit-log* and proposes diffs.

**Define once, reuse across:** a **shared tool-pack** (`bash · edit · fs · deploy · http ·
scaffold_agent`) is written once and allowlisted per agent. **Governance lives in the tools** (the
`deploy` tool refuses an unlocked-auth deploy), which makes the safety gate portable across every
runtime instead of bolted to one harness's hook.

## The Forge — create + evolve

The Forge is the primitive configured to *emit the primitive*; its product is a per-user agent
expressed as **data** — a workspace directory, not hand-written code. Two jobs:

1. **Create** — absorb a user's artifacts (a template + a transcript + an example), ask ≤3
   questions, produce a working agent, show a first-output preview.
2. **Evolve** — read the agent's edit/correction log and propose workspace diffs, tested against
   the agent's own frozen fixtures before anything reaches the user.

## Gated self-evolution (the differentiator)

"Improves and personalizes itself" is the headline feature and the biggest risk, so it is designed
as **gated evolution** — a stop-gradient discipline:

1. **Append-only episodic log** — every interaction, correction, and edit-diff. Never mutated.
2. **Derived layer** — the skills/rules/memory the agent runs on, provenance-linked back.
3. **The loop** — propose a diff → test against frozen fixtures → surface at **the gate** ("I
   learned X. Approve?") → user approves → committed as a versioned, revertable diff.

The agent never free-form self-modifies live. The user's approval is the causally-independent
verification signal; replay-against-frozen-substrate is what makes consolidation safe.

## The surface

Built on the **Broomva Design System** (see [`../design-system/`](../design-system/)) — a calm,
monochrome, cool-blue design language for work-orchestration agents. Its load-bearing inventions:
**the Composer** (the one input), **the gate / the look** (a session compressed to *made · decided
· asks*, with approve / edit as the only controls), **Receipts** (evidence over progress bars),
**the Undertow** (a running signal — presence, not progress), and the plain-voice **WorkState**
vocabulary (Queued · Running · Needs you · Done · Standing). Interactive mockups live in
[`../prototypes/`](../prototypes/).

## The record — own-the-record on a rented runtime

State splits by lifecycle, and the moat lives in the record:

| Store | Holds | Owner |
|---|---|---|
| **git / FS** `workspaces/<user>/<agent>/` | the agent's definition + memory + skills | **you (the moat)** |
| **DB** (Postgres) | identity + tenant map + the append-only event log | you |
| runtime session log | in-flight execution (HITL park/resume) | the runtime |
| object store | uploads + rendered outputs | you |

The workspace is Ember's **system of record in a portable, S3-compatible store** — not the
runtime's ephemeral sandbox. Per run, the runtime **FUSE-mounts** it into the sandbox as
`/workspace/<user>` (no copy); reads hydrate via the mount, and the evolve loop's write-back
(gated diffs) commits through Ember's own git/DB path. So even fully on a rented runtime, the
record is in a store you own — and can move.

## Runtime — eve, behind the seam

The runtime is **eve on Vercel** (durable sessions, HITL, channels, AI Gateway model routing,
FUSE-mounted workspaces), placed behind an `ExecutionHost` seam so it stays swappable. The engine
is model-agnostic: cheap/open models for high-frequency work, stronger models for hard cases, all
via the gateway.

## Voice & capture

Capture is the front of the loop (capture → structure → generate → file). Text/paste is v1; **voice
is first-class**:

- **Live in-app voice** — a realtime hook (barge-in, tool-calling mid-reply). The user talks
  through the task; the agent fills the result live. Barge-in corrections are evolve signal.
- **Async voice notes** — speech-to-text → agent → reply. Near-zero behavior change for the long
  tail.

## Conventions

bun · Biome · Better Auth (never NextAuth) · Next.js (installable PWA) · eve on Vercel · AI Gateway.
Governed by [bstack](https://github.com/broomva/bstack) (see [`../CLAUDE.md`](../CLAUDE.md)).
