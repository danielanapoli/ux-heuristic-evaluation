# Workflow

**Phases must be completed in order. Do not score severity (Phase 5) before completing expert reconciliation (Phase 4). Do not write the executive summary before all issues are cataloged.**

## Phase 1 — Ingest, restate, and calibrate

Restate the artifact, scope, target user, and primary tasks back to the requester. Surface assumptions explicitly.

Calibrate RPN bands to the product category; write chosen bands into the methodology note before scoring begins.

If this is a follow-up pass, apply the [Follow-up / Delta Pass Protocol](./follow-up-protocol.md) before continuing.

## Phase 2 — Walkthrough & candidate issues

Walk each in-scope journey step by step. For each step, ask:

- What does the system communicate?
- What does the user have to know, remember, or infer?
- Where could a user get stuck, confused, or make an error?
- What happens when things go wrong?

Generate candidate issues. **Do not score severity yet.**

### Verification escalation — rendered behavior

Verify before promoting a candidate to the catalog if it rests on any of:

- An `href` that appears empty, anchor-only (`#`), or non-functional.
- A section that appears empty in static HTML but might be client-rendered.
- An internal link pointing to a route whose existence is uncertain.
- Hover/focus/active states, animation, or any interaction.
- Accessibility attributes (`alt`, `aria-*`, label associations) that appear missing.

**Escalation paths, in order:**
1. Open in a rendered browser (e.g., Claude in Chrome) and observe directly.
2. Make a HEAD request to the suspect URL.
3. Re-fetch with a different parsing path that preserves attributes.

If verification is impossible, downgrade to Quality Issue (flagged "requires verification") or Design Observation. Do not file an unverified claim as a Heuristic Violation.

### Verification escalation — freshness

Static HTTP fetch tools can return cached or stale content without warning. Treat stale fetch as one of the most dangerous failure modes — every downstream artifact inherits the staleness.

**Triggers that demand freshness verification:**
- Follow-up or delta pass after the requester reported changes (always verify).
- New fetch returns content byte-identical (or near-identical) to a prior session's fetch.
- Requester contradicts a filed finding.
- Visible "Last updated" date, build hash, or version is older than the requester's reported change date.
- Fetched content references elements the requester says were removed or renamed.

**Methods, in order of preference:**
1. **Render in a real browser** (e.g., Claude in Chrome) — bypasses fetch-tool caches, exercises real DOM.
2. **Append a cache-busting query parameter** (e.g., `?nocache={timestamp}`) if the fetch tool supports it.
3. **Compare on-page recency signals** (visible `Last updated`, version strings) against the requester's reported change date.
4. **Ask the requester to confirm** one specific element as a freshness fingerprint.

**If freshness cannot be verified:** state the cache uncertainty in the report and default to trusting the requester's direct observation over fetched content.

## Phase 3 — Heuristic mapping or bucket assignment

Assign each candidate to one bucket per [frameworks.md](./frameworks.md).

Before filing as a Heuristic Violation, state: *which specific heuristic is violated, and what observable behavior causes the violation?* If you cannot answer both in one sentence, reassign to Quality Issue.

## Phase 4 — Expert reconciliation

Bring 2–4 panelists' lenses to each issue per [expert-lenses.md](./expert-lenses.md). Note agreement, disagreement, and reframing.

## Phase 5 — Dual severity scoring

Score on both FMEA and Nielsen per [severity-systems.md](./severity-systems.md). Compute RPN. Use the calibration anchors to cross-check scores before filing. Flag discrepancies between FMEA and Nielsen.

## Phase 6 — Contextualization

Categorize each issue's prevalence: Novel / Common / Well-documented anti-pattern. Cite real sources only; otherwise: *"no benchmark cited; expert judgment only."*

## Phase 7 — Panel balance review

1. Tally per-panelist and per-cluster citations.
2. Apply thresholds: no panelist over ~50%, no cluster over ~40%; every cluster cited at least once.
3. Revisit flagged issues and rebalance where another lens fits at least as well.
4. Re-tally and confirm thresholds met.
5. Record the completed tally in Appendix E using this structure:

| Cluster | Members cited | Citation count | % of total | Threshold met? |
|---|---|---|---|---|
| Foundations | | | | |
| Clarity | | | | |
| Structure | | | | |
| Behavior & research | | | | |
| Measurement | | | | |
| Ethics & inclusion | | | | |

## Phase 8 — Synthesis

Cluster issues by theme. Identify systemic vs. surface-level problems. Write the executive summary last.

## Phase 9 — Defensibility audit (pre-ship)

Run this audit before delivery. Record result in Appendix F. Fix any failure before delivering.

1. **Citations** — every cited source is real and verifiable, or marked "expert judgment only."
2. **Simulated quotes** — every quote labeled simulated.
3. **Reproducibility** — every issue has steps specific enough for a third party.
4. **Score justifications** — every FMEA dimension and Nielsen severity has reasoning; cross-checked against calibration anchors.
5. **Rendered-behavior verification** — no Heuristic Violation rests on unverified rendered behavior.
6. **Freshness verification** — for follow-up passes, freshness verified per methods above; for first passes, no byte-identical refetch treated as current.
7. **Discrepancies surfaced** — FMEA-vs-Nielsen and inter-expert disagreements explained.
8. **Panel balance** — Appendix E tally complete with counts and percentages; thresholds met or deviations justified.
9. **Scope honesty** — pages or features not evaluated are listed.
10. **Calibration disclosed** — RPN band calibration is in the methodology note.
11. **Fallback inputs disclosed** — missing inputs documented and confidence calibrated.
12. **Fetch method disclosed** — rendered browser or static fetch noted in Methodology Note; static fetch limitation flagged if applicable.