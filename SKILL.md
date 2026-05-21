---
name: ux-heuristic-eval
description: Conduct a comprehensive, defensible, expert-led usability heuristic evaluation of a website
disable-model-invocation: true
---

# UX Heuristic Evaluation

## Instructions

When user asks to run a heuristic evaluation, follow this document strictly. If the requester directly contradicts a finding, treat their observation as correct by default and investigate the source of your fetched view.

## Methodology Overview (read all documentation before starting)

1. Walk through the product methodically as a user would. Refer to [workflow.md](./references/workflow.md) for the phase-by-phase process.
2. Identify issues grounded in two foundational frameworks. Refer to [frameworks.md](./references/frameworks.md).
3. Reason about each issue through a simulated panel of named UX experts. Refer to [expert-lenses.md](./references/expert-lenses.md).
4. Score each issue with two severity systems. Refer to [severity-systems.md](./references/severity-systems.md).
5. Produce a structured, auditable report as defined in [report-guidelines.md](./references/report-guidelines.md).

You are **not** a substitute for real user testing or live expert review. Say so in the methodology note.

---

## Required Inputs

⛔ **Do not begin Phase 1 until blocking inputs are confirmed. Inferring silently is not a substitute for asking.**

**Blocking — must confirm before starting:**
- **Artifact under review** — URL, prototype, screenshots, or description. List every assumption if access is limited.
- **Primary user(s)** — who they are, what they know, context of use.
- **Top tasks / user journeys** — what users are trying to accomplish.

**Non-blocking — confirm if possible; document gap if not:**
- **Scope** — which screens, flows, or features are in vs. out.
- **Business context** — what the product does, its goal, its stage (concept, MVP, mature).
- **Product category** — transactional, informational, portfolio, safety-critical, etc. Calibrates RPN bands per [severity-systems.md](./references/severity-systems.md).
- **Prior research** — surveys, interviews, analytics, support tickets. Informs but does not replace evaluation.
- **Is this a follow-up pass?** If yes, confirm what changed and when. Triggers [Follow-up / Delta Pass Protocol](./references/follow-up-protocol.md).
- **Output format** — Markdown (default), Word doc, PDF, slide deck.

### Fallback when non-blocking inputs are unavailable

If the requester is genuinely unable to supply non-blocking inputs after being asked:

1. Document the gap explicitly in the methodology note.
2. Infer carefully from the artifact; surface every inference as an assumption.
3. Calibrate confidence downward for any issue whose severity rests on the missing input.
4. List the inputs that would sharpen the evaluation at the top of the report.

---

## Defensibility Rules (non-negotiable)

- **No fabricated citations.** Real or "expert judgment only."
- **Simulated expert quotes are labeled as such.**
- **Distinguish evidence from judgment** throughout.
- **Every issue is reproducible** with concrete steps.
- **Every severity score is justified.**
- **Discrepancies are surfaced, not smoothed.**
- **Scope is honest.** Not-evaluated items are listed.
- **Verification before claim.** Rendered-behavior claims are verified.
- **Freshness before claim.** Content currency is verified before filing findings on follow-up passes.
- **Calibration is disclosed.**
- **Requester observation outranks agent fetch.** When the agent's fetched view conflicts with the requester's direct observation, the requester is correct by default. Investigate the discrepancy (cache, parser artifact, deploy lag, environment mismatch) before filing anything.

---

## Kickoff Checklist

- [ ] Blocking inputs confirmed: artifact, primary user(s), top tasks.
- [ ] Non-blocking inputs confirmed or gaps documented.
- [ ] Assumptions surfaced in writing.
- [ ] Product category confirmed; RPN bands calibrated, or gap documented.
- [ ] Fetch method noted: rendered browser (preferred) or static fetch. If static, limitation flagged in Methodology Note.
- [ ] **First pass or follow-up confirmed. If follow-up, [Follow-up / Delta Pass Protocol](./references/follow-up-protocol.md) applied before any scoring.**
- [ ] **If follow-up: freshness fingerprint established before any fetch. Methods in order: (1) render in real browser, (2) cache-busting query param, (3) compare on-page recency signals, (4) ask requester to confirm one specific element. Do not file findings until freshness is confirmed.**
- [ ] Panel balance review run per [workflow.md](./references/workflow.md); tally recorded in Appendix E.
- [ ] Defensibility audit run (Phase 9); result recorded in Appendix F.
- [ ] Report produced in requested format.