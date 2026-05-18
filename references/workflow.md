# Workflow 
 
## Phase 1 — Ingest, restate, and calibrate
 
Restate the artifact, scope, target user, and primary tasks back to the requester. Surface assumptions explicitly.
 
**Calibrate the RPN bands** to the product category and write the chosen bands into the methodology note before scoring begins.
 
If this is a follow-up pass, jump to the [Follow-up / Delta Pass Protocol](./follow-up-protocol.md) before continuing.
 
## Phase 2 — Walkthrough & candidate issues
 
Walk each in-scope journey step by step. For each step, ask:
 
- What does the system communicate?
- What does the user have to know, remember, or infer?
- Where could a user get stuck, confused, or make an error?
- What happens when things go wrong?

Generate candidate issues. **Do not score severity yet.**
 
### Verification escalation — rendered behavior
 
If a candidate issue rests on any of the following, **verify before promoting it to the catalog** — do not ship a caveat in place of evidence:
 
- An `href` appears empty, anchor-only (`#`), or non-functional.
- A section appears empty in static HTML but might be client-rendered.
- An internal link points to a route whose existence is uncertain.
- The claim depends on hover/focus/active states, animation, or any interaction.
- Accessibility attributes (`alt`, `aria-*`, label associations) appear missing.

**Escalation paths**, in order:
 
1. Open the artifact in a rendered browser (e.g., Claude in Chrome) and observe directly.
2. Make a HEAD request to the suspect URL.
3. Re-fetch with a different parsing path that preserves attributes.

If verification is impossible, downgrade the candidate to Quality Issue (flagged "requires verification") or Design Observation. Do not file an unverified claim as a Heuristic Violation.
 
### Verification escalation — freshness
 
Static HTTP fetch tools can return **cached or stale content** without warning. A stale fetch silently treated as current is one of the most dangerous failure modes for this kind of evaluation — every downstream artifact (issues, scores, reproduction steps, recommendations) inherits the staleness.
 
**Triggers that demand freshness verification:**
 
- This is a follow-up or delta pass after the requester reported changes (always verify).
- A new fetch returns content byte-identical (or near-identical) to a prior session's fetch of the same URL.
- The requester contradicts a finding you filed.
- A visible "Last updated" date, build hash, or deploy version on the page is older than the requester's reported change date.
- Fetched content references elements (labels, copy, components) that the requester has explicitly said were removed or renamed.

**Methods, in order of preference:**
 
1. **Render the artifact in a real browser** (e.g., Claude in Chrome) — most reliable because it bypasses fetch-tool caches and exercises the real DOM.
2. **Append a cache-busting query parameter** to the URL (e.g., `?nocache={timestamp}`), if the fetch tool supports arbitrary URLs.
3. **Compare on-page recency signals** (visible `Last updated` dates, version strings) against the requester's reported change date.
4. **Ask the requester to confirm** the current state of one specific element you can use as a freshness fingerprint (e.g., "Can you confirm whether `Tools (coming soon)` is currently in the nav on /user-research?").

**If freshness cannot be verified:**
 
- Do not file delta findings that contradict the requester's direct observation.
- State the cache uncertainty explicitly in the report.
- Default to trusting the requester's direct observation over your fetched content.

##  Phase 3 — Heuristic mapping or bucket assignment
 
For each candidate, choose one of the buckets identified in [frameworks.md](./frameworks.md). Do not force a Quality Issue into a heuristic mapping to keep it in the main catalog.
 
## Phase 4 — Expert reconciliation
 
Based on the UX expert perspective described in [expert-lenses.md](expert-lenses.md) bring 2–4 panelists' lenses to each issue. Note agreement, disagreement, and reframing.
 
## Phase 5 — Dual severity scoring
 
Based on [severity-systems.md](./severity-systems.md) score on both FMEA and Nielsen. Compute RPN. Flag discrepancies. 
 
## Phase 6 — Contextualization
 
For each issue, categorize prevalence: Novel / Common / Well-documented anti-pattern. Cite real sources only. Otherwise: *"no benchmark cited; expert judgment only."*
 
## Phase 7 — Panel balance review
 
After all issues are drafted, scored, and contextualized:
 
1. **Tally** per-panelist and per-cluster citations.
2. **Apply thresholds:** no panelist over ~50%, no cluster over ~40%; every cluster cited at least once.
3. **Revisit flagged issues** and rebalance where another lens fits at least as well.
4. **Re-tally** and confirm thresholds met.
5. **Record the tally in Appendix E.**

## Phase 8 — Synthesis
 
Cluster issues by theme. Identify systemic vs. surface-level problems. Write the executive summary last.
 
## Phase 9 — Defensibility audit (pre-ship)
 
Before delivering the report, run this audit and **record the result in Appendix F**.
 
1. **Citations.** Every cited source is real and verifiable; otherwise marked "expert judgment only."
2. **Simulated quotes.** Every quote is labeled simulated.
3. **Reproducibility.** Every issue has steps to reproduce specific enough for a third party.
4. **Score justifications.** Every FMEA dimension and Nielsen severity has reasoning.
5. **Verification status (rendered behavior).** No Heuristic Violation rests on unverified rendered behavior.
6. **Verification status (freshness).** For follow-up passes, freshness has been verified (rendered browser, cache-busting URL, on-page recency signal, or requester confirmation). For first passes, the agent confirms no byte-identical refetch was treated as current (see Verification escalation — freshness, above).
7. **Discrepancies surfaced.** FMEA-vs-Nielsen and inter-expert disagreements are explained.
8. **Panel balance.** Tallies reconcile; thresholds met or deviations justified.
9. **Scope honesty.** Pages or features not evaluated are listed.
10. **Calibration disclosed.** RPN band calibration is in the methodology note.
11. **Fallback inputs disclosed.** Missing inputs are documented and confidence calibrated.

If any check fails, fix it before delivery.
