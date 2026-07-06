---
name: broomva-design
description: Use this skill to generate well-branded interfaces and assets for Broomva, the work-orchestration AI agent product, either for production or throwaway prototypes/mocks/etc. Contains the philosophy (work is the noun, the orchestrator is an agent), essential design guidelines, colors, type, fonts, assets, and UI kit components for prototyping. Broomva's visual language is a calm monochrome philosophy on a blue axis — barely-blue ink instead of black, frosted liquid-glass blue in accents and shadows, glass earned only by overlays, popovers and the composer, and the Undertow as the live running signal.
user-invocable: true
---

# Broomva design skill

Read the `readme.md` file within this skill, and explore the other available files (`styles.css`, `tokens/`, `assets/`, `components/` — core, forms, navigation, overlays, work — `apps/maestro/` (the Broomva app), `templates/`, `guidelines/`).

If creating visual artifacts (slides, mocks, throwaway prototypes, etc), copy assets out and create static HTML files for the user to view. If working on production code, you can copy assets and read the rules here to become an expert in designing with this brand.

If the user invokes this skill without any other guidance, ask them what they want to build or design, ask some questions, and act as an expert designer who outputs HTML artifacts _or_ production code, depending on the need.

## The philosophy

Broomva orchestrates loops of agentic workflows under structure: control, governance, and bio-inspired principles of metacognition, persistence, stability and flow. Autonomy is the moat; control is the engine. **The scarce resource is unsupervised hours** — not tokens, not compute: how long an agent runs before a human must look. The design language exists to make that legible and calm.

- **The workspace is the substrate.** An FS + sh environment. A folder is work at any scale — question, task, project, initiative; depth is meaning, not schema. Frontmatter is the orchestration contract (kind, state, owner, budget, gate), living in the files.
- **The session is the verb.** A running agent timeline of events (agent, user, tools). Anything spawns one: you, the orchestrator, another session. Work is the noun; sessions do the work.
- **Chat is a projection.** A session renders the work; it never owns it. The same run can appear in a side panel, a thread, or a handoff page.
- **The orchestrator is an agent.** A session that schedules sessions. It has presence (a live signal in the chrome), a session you can open, and a wake log — never a settings page. Setting a schedule is a sentence.
- **The tick is a prompt.** Wakes have causes: a worker returning, your message, an interval, a self-set routine. The loop is legible — show why it woke.
- **The branch is the receipt.** Evidence over claims: `run/<id>`, diffstats, judge verdicts. Never fake progress percentages.
- **The gate is yours.** No loop can auto-Done. Clean runs wait at "Needs you"; approving is the one human verb. Needing you is a gate, not a failure — mark halts in accent-blue, never red.
- **The look is the transaction.** Hours of agent work compress to: what changed · what it decided · what it asks. Autonomy is bought with good looks — a fast, confident look earns the next longer unsupervised run.
- **Standing loops never close.** Open-ended problems are folders with a cadence (`kind: routine`); the routine is the deliverable. `gate: none` spends zero human hours until a run flags something.
- **Calm is load-bearing.** Live signals breathe, they don't spin for attention. Motion encodes presence, not urgency.

## Quick reference

- **Look:** barely-blue ink `oklch(0.175 0.022 265)` on white. Cool monochrome (every gray sits at hue 265). Whisper borders at 7% blue-black. Dark mode is a deep blue-purple `oklch(0.135 0.02 272)`, fully specified.
- **Type:** system fonts, 12 / 14 / 16 / 18 / 22 / 24 / 28px. Regular (400) default; medium (500) buttons. CalSans is opt-in for hero/marketing headings only (`data-display-font="calsans"`).
- **Work states:** plain voice is canon — Queued · Running · Stuck · Needs you · Done (plus Standing for routines). System enums (Todo, InProgress, Blocked, InReview) are a developer surface only. The dot carries the color: gray / info / warning / accent-blue / success.
- **The inspector pattern:** selection drives both surfaces — the plane shows the work inside, the panel shows the contract and the sessions doing it. Item → look/chat/activity · folder → frontmatter + sessions · routine → frontmatter + runs.
- **The disclosure ladder:** the substrate is for agents; the user gets signals, verbs, and receipts. Rung 1 ambient (feed, chip, bench, Undertow) → rung 2 the gate (the look; control is verbs — approve, send back, grant, point) → rung 3 receipts (inspector; for verifying, never for operating). Fully operable from rungs 1–2; never show worktrees, index.db, or the engine room. See `guidelines/disclosure.html`.
- **Keep score in unsupervised hours:** the autonomy scoreboard (hours today, a notch per human look) and per-session unsupervised durations — never percentages.
- **Buttons:** pill-shape. Primary = ink fill (`--primary`), hover lightens one step. Secondary = card bg + 16% border. Hover on ghost/soft = frosted blue (`--bv-frost-8`).
- **Focus:** always ai-blue `--bv-blue` (`--ring`), never black.
- **Glass:** ONLY overlays, popovers, and the composer (`.bv-glass`, `.bv-glass-heavy`, `.bv-glass-composer`). Every glass surface has the inner light line. Cards, panels, chrome: matte.
- **Composer:** `rounded-[28px]` glass + the frosted-blue halo (`--bv-shadow-composer`) — the one dramatic depth cue.
- **Color use:** monochrome by default. Color = status, agent avatars, the Undertow live signal, inline assistant link pills, and the frosted-blue interaction layer (hover/selected/focus/glow).
- **Live signal:** the Undertow (`.bv-undertow` + `.bv-undertow-orbit`, in `tokens/motion.css`) is THE running treatment — a contained 4px halo of breathing pools, a counter-phase tide, and a faint 9s orbit. The tidepool dot (`.bv-dot-live`) carries the same weather at dot scale — status dots, list rows, the bench. The border comet and the orbiting dot comet are retired.
- **Icons:** Lucide (CDN). 20px standard, 2px stroke, `currentColor`. No other libraries, no emoji-as-icons.
- **Motion:** under 300ms for feedback. Signature live signals: Undertow, dot comet, typing-bounce. Layered rhythms over loops; no bouncy entrances; everything stops under reduced motion.
- **Components:** core atoms (Button, IconButton, Input, Card, StatusBadge, Avatar, Composer, DotComet), forms (Select, Checkbox, Radio, Switch, Textarea, Field), navigation (Tabs, Segmented, CommandPalette), overlays (Dialog, Menu, Tooltip, Toast — the glass-earning surfaces), and the work primitives (WorkState, LifecycleRail, Receipt, Undertow, RunCard, AutonomyScoreboard). Compose these; don't re-implement them.
- **Voice:** plain-language, second-person, sentence case. "Needs you" not "In Review". No emoji. No em dashes. No uppercase eyebrows.

## Don't

- Don't use pure `#000` or pure-white text in dark mode. All colors are OKLCH.
- Don't put glass on cards, sidebars, or chrome. Glass is earned by floating surfaces only.
- Don't invent new hues. ai-blue (260) is the accent; accent-blue (235) only when two accents must coexist (it owns "Needs you").
- Don't use the retired border comet for running work — running work wears the Undertow; status dots wear the dot comet.
- Don't add orange/yellow to live signals — Broomva runs blue → indigo → cyan → ice.
- Don't show progress percentages on agent work. Show receipts: branch, diffstat, judge verdict, event timeline.
- Don't give the orchestrator a settings page or hide it behind system buttons. It's an agent: presence in the chrome, a session you open, schedules set in a sentence.
- Don't use CalSans in app chrome.
- Don't write Title Case labels, UPPERCASE eyebrows, or wide letterspacing.
- Don't use warm grays — every neutral sits on the cool axis.
- Don't use scale/rotation/glow on hover. Hover is a frosted-blue fill or a one-step lighten.
