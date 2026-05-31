# The Agentic Architect — Journey

An interactive, self-contained learning app that takes a technical professional from *"what is an agent?"* to *reviewing an enterprise agentic design under security, data, responsible-AI, and NFR gates.*

It is a single HTML file. No build step, no server, no dependencies to install. Open it in a browser and it runs.

> © 2026 **Aniket Mukherjee**. All rights reserved.

---

## What it is

A gated, milestone-based curriculum built for **architects and senior engineers**, structured as two tracks:

- **Foundation (6 levels)** — the mental models. For a technical professional new to agentic AI.
- **Architect (9 levels)** — enterprise design discipline. For people who already hold distributed systems, security, and SDLC, and need the *agentic delta*.

Each level follows the same loop: **Briefing → applied Challenge → Quiz → Unlock.** A level only opens when the previous one is passed (70% on both the challenge and the quiz). Progress and XP are tracked.

A **test-out diagnostic** on the landing screen lets a fluent practitioner skip Foundation and unlock the Architect track directly (4 of 5 to pass).

The teaching emphasis throughout is judgement, not vocabulary: most challenges are *diagnose-the-flaw* and *make-the-design-decision*, with the tempting wrong answers drawn from real anti-patterns.

---

## How to run it

1. Download `Agentic_Architect_Journey_v0.6.html`.
2. Double-click it, or open it in any modern browser (Chrome, Edge, Firefox, Safari).

That's all. It is fully offline once loaded (web fonts load from Google Fonts if online; it degrades gracefully to system fonts if not).

### Progress persistence — important

Progress and XP are saved in the browser's `localStorage`, keyed per device/browser.

- **Opened as a downloaded file or hosted on a normal web server → progress persists** across sessions. This is the intended way to use it.
- **Viewed inside a sandboxed preview (e.g. embedded in a chat window) → it runs fully, but progress is in-memory only** and resets on refresh.

There is no backend. Nothing is sent anywhere. A **Reset** control in the top bar clears all progress on the current device.

---

## Curriculum

### Foundation track

| # | Level | Challenge type |
|---|-------|----------------|
| F1 | Model, Workflow, or Agent? | Classify |
| F2 | The Agent Loop & Its Action Surface | Diagnose |
| F3 | Non-Determinism: "It Worked Once" ≠ "It Works" | Predict |
| F4 | Memory: The Highest-Leverage Liability | Find the flaw |
| F5 | The Autonomy / Oversight Dial | Assign |
| F6 | Capstone — Design a Safe Support Assistant | Integrative (5/6 to pass) |

### Architect track

| # | Level | Challenge type |
|---|-------|----------------|
| A1 | Pattern Selection — and When NOT to Use an Agent | Select the pattern |
| A2 | Multi-Agent Topologies & the Coordination Tax | Diagnose the topology |
| A3 | Tool & Integration Architecture | Find the integration flaw |
| A4 | Data & Context Architecture | Find the grounding flaw |
| A5 | Threat Modelling — OWASP Agentic Top 10 | Name the threat |
| A6 | Guardrails, Autonomy Tiers & Kill-Switches | Fix the control gap |
| A7 | Responsible AI by Design | Spot the RAI failure |
| A8 | Observability, Evals & Cost — NFRs as Gates | Set the gate |
| A9 | Architect Capstone — Full Design Review | Integrative (7/10 to pass) |

*(Internally the level IDs are `f1–f6` and `a1, a2, a3, adata, a4, a5, arai, a6, a7`; the table above shows display order.)*

### Design principles woven through every level

Minimal agency (the simplest pattern that solves the problem), guardrails enforced **outside** the model, autonomy proportioned to consequence and reversibility, memory and context as liabilities to design first, tested fail-safe kill-switches as a precondition of go-live, and **NFRs as pass/fail gates** rather than prose — latency budget, cost ceiling, auditability, failure containment.

---

## What it's grounded in

The content is domain-agnostic but grounded in public industry canon, not invented:

- **Agent/workflow pattern vocabulary** — augmented LLM, prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer; the discipline of preferring a workflow to an agent.
- **OWASP Top 10 for Agentic Applications (2026)** — ASI01–ASI10, with real 2025 incident framing.
- **Multi-agent coordination cost** — the token/latency penalty and the read-vs-write parallelisation heuristic.
- **MCP, gateway/registry pattern, least privilege** — tool-description poisoning, rug-pulls, supply-chain risk.
- **Context engineering & RAG** — just-in-time retrieval, grounding as the hallucination lever, context/retrieval poisoning.
- **Responsible AI frameworks** — EU AI Act risk tiers, NIST AI RMF (Govern/Map/Measure/Manage), ISO/IEC 42001.

### A note on freshness

Durable principles (minimal agency, defence-in-depth, plan-then-validate, memory/context hygiene, kill-switches, NFR gates) are stable. The **tooling and regulatory layer moves fast** — MCP maturity, the framework landscape, and especially regulatory timelines. As one example, the EU AI Act's high-risk obligation deadline was in active flux as of mid-2026 (a proposed Omnibus deferral toward December 2027 had been provisionally agreed but not formally adopted). For that reason specific dates were deliberately kept out of quiz answers. Treat the tooling/regulatory references as swappable examples and plan a periodic content review.

---

## Customising the content

All levels live in two JavaScript arrays near the top of the `<script>` block: `FOUNDATION` and `ARCHITECT`. Each level is a plain object:

```js
{
  id: 'a1',
  ctype: 'Select the pattern',     // small label shown on the card
  title: '...',
  desc: '...',                     // one-line description on the map
  cpass: 5,                        // optional: challenge pass threshold (defaults to 70%)
  brief:    [ { h, p:[...], li:[...], callout, svg } ],  // briefing blocks; svg is an optional inline-SVG string rendered under the block
  challenge:[ { q, o:[...], c, e } ],               // c = index of correct option, e = explanation
  quiz:     [ { q, o:[...], c, e } ]
}
```

To edit text, change a string. To add a question, add an object to `challenge` or `quiz`. To add a level, add an object to the array — the map, gating, and progress logic pick it up automatically. The test-out diagnostic is the separate `TESTOUT` object.

No framework knowledge is required to edit content; it is vanilla HTML/CSS/JS.

---

## Design & theming

- Original logomark: three connected nodes forming a triangle-with-crossbar — reads as an **"A"** and as an orchestrator-and-two-workers topology.
- Briefing diagrams are hand-built inline SVG in the same palette (no image files, no scripts), added per block via the optional `svg` field.
- Vibrant light theme (violet → magenta → blue spectrum); no dark/black background.
- Colours are defined as CSS custom properties in `:root` (`--violet`, `--magenta`, `--blue`, etc.), so the palette can be retuned in one place.
- Fonts: Bricolage Grotesque (display), Hanken Grotesk (body), JetBrains Mono (labels).

---

## Version history

| Version | Change |
|---------|--------|
| v0.1 | Vertical slice: landing, test-out diagnostic, full Foundation track (6 levels). |
| v0.2 | Added the full Architect track (then 7 levels); track-aware gated map. |
| v0.3 | Added copyright attribution (source header + visible footer). |
| v0.4 | Replaced the placeholder mark with an original logomark and network motif. |
| v0.5 | Added **A4 Data & Context Architecture** and **A7 Responsible AI by Design**; capstone expanded to 10 decisions. **15 levels total.** |
| v0.6 | Embedded **8 briefing diagrams** (inline SVG, in-theme): F1 autonomy ladder, F2 agent loop, F5 oversight spectrum, A1 pattern-selection decision, A2 single-vs-orchestrator topology, A3 tool gateway, A4 grounding pipeline, A6 autonomy tiers. Renderer extended with an optional per-block `svg` field — additive, non-breaking. |

---

## Known limitations / possible next steps

- **Diagram coverage is selective** — eight briefings carry diagrams (see v0.6). The remaining levels are deliberately text-only where a visual would be decoration rather than teaching (e.g. the OWASP Top 10 list in A5, the pillar lists in A7/A8, and the capstone decision exercises). The strongest remaining candidate is an F4 memory diagram (short-term vs long-term with a poisoned write surviving into a later session).
- **Single-file, single-author content** — no CMS; content edits are made directly in the file.
- **No completion certificate or export** — could be added.
- **Foundation is intentionally lean** — RAG/grounding is taught in the Architect track only; a light Foundation primer was deliberately omitted to keep the beginner track short.

---

## License

© 2026 Aniket Mukherjee. All rights reserved. 

*A copyright notice asserts ownership but is not itself legal protection. If this will be distributed beyond your control, seek appropriate legal advice on licensing.*
