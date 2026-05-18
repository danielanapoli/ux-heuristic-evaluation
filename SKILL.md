
---
name: ux-heuristic-eval
description: Conduct a comprehensive, defensible, expert-led usability heuristic evaluation of a website
disable-model-invocation: true
---

# UX Heuristic Evaluation

## Instructions

When user asks to run a heuristic evaluation of a specific website, follow the process outlined in this document. When running the evaluation, adhere strictly to the methodology and defensibility rules. Always verify freshness on follow-up passes and when fetched content matches a prior session's fetch byte-for-byte. If the requester directly contradicts a finding, treat their observation as correct by default and investigate the source of your fetched view.

## Methodology Overview (read all documentation before starting)

1. Walk through the product/artifact methodically as a user would, noting any issues or friction points. Refer to [workflow.md](./references/workflow.md) for a detailed phase-by-phase process.
2. Identify issues grounded in two foundational frameworks. Refer to [frameworks.md](./references/frameworks.md).
3. Reasoning about each issue through the lens of a simulated panel of named UX experts. Refer to [expert-lenses.md](./references/expert-lenses.md).
4. Scoring each issue with two distinct severity systems. Refer to [severity-systems.md](./references/severity-systems.md).
5. Produce a structured, auditable report as defined in [report-guidelines.md](./references/report-guidelines.md) that explicitly flags its own limits.

You are **not** a substitute for real user testing or live expert review. Say so in the methodology note. Never claim user research findings you don't have.
 
---
 
## Required Inputs (ask before starting if missing, do not make assumptions)
 
Before running the evaluation, confirm:
 
- **Artifact under review** — URL, prototype link, screenshots, video, or written description. If access is limited, list every assumption you're making.
- **Primary user(s)** — who are they, what do they know, what's their context of use?
- **Top tasks / user journeys** — what are users trying to accomplish?
- **Scope** — which screens, flows, or features are in vs. out of scope?
- **Business context** — what does the product do, what's the goal, what stage is it at (concept, MVP, mature)?
- **Product category** — transactional, informational, portfolio, safety-critical, etc. This calibrates the RPN bands defined in [severity-systems.md](./references/severity-systems.md).
- **Prior research, if any** — surveys, interviews, analytics, support tickets. Use these to inform but not replace your evaluation.
- **Is this a follow-up pass?** If yes, confirm what changed since the prior evaluation and when the changes deployed. This triggers the [Follow-up / Delta Pass Protocol](./references/follow-up-protocol.md).
- **Output format** — Markdown (default), Word doc, PDF, slide deck.

If any of these are missing, ask before proceeding. Do not invent context.
 
### Fallback when inputs are unavailable
 
If the requester cannot supply some inputs, do **not** invent them and do **not** stall. Proceed as follows:
 
1. **Document the gap explicitly** in the methodology note.
2. **Infer carefully** from the artifact itself; surface every inference as an assumption.
3. **Calibrate confidence downward** for any issue whose severity rests on the missing input.
4. **List the inputs that would sharpen the evaluation** at the top of the report.

## Defensibility Rules (non-negotiable)
 
- **No fabricated citations.** Real or "expert judgment only."
- **Simulated expert quotes are labeled as such.**
- **Distinguish evidence from judgment** throughout.
- **Every issue is reproducible** with concrete steps.
- **Every severity score is justified.**
- **Discrepancies are surfaced, not smoothed.**
- **Scope is honest.** Not-evaluated items are listed.
- **Verification before claim.** Rendered-behavior claims are verified.
- **Freshness before claim.** For follow-up passes, content currency is verified before filing findings.
- **Calibration is disclosed.**
- **Requester observation outranks agent fetch.** When the agent's view of the artifact (via WebFetch, static HTML, screenshot, or any intermediary) conflicts with the requester's direct observation of the live product, the requester is correct by default. The agent must investigate the source of the discrepancy (cache, parser artifact, deploy lag, environment mismatch) rather than defend the fetched view. Filing findings that contradict a direct requester observation without first ruling out a stale or wrong-source fetch is a serious defensibility failure.

## Kickoff Checklist
 
- [ ] I have the artifact or sufficient description.
- [ ] I know the primary user and top tasks.
- [ ] I have agreed scope with the requester.
- [ ] I know the product category and have calibrated RPN bands.
- [ ] I have surfaced assumptions in writing.
- [ ] If required inputs are missing, I have documented the gap and chosen a fallback.
- [ ] **I have confirmed whether this is a first pass or follow-up. If follow-up, I have applied the [Follow-up / Delta Pass Protocol](./references/follow-up-protocol.md) before any scoring or filing.**
- [ ] I have re-read the two heuristic frameworks.
- [ ] I have the expert panel lenses fresh.
- [ ] I have the two severity rubrics ready.
- [ ] I will use the three-bucket structure honestly.
- [ ] I will escalate verification for any claim depending on rendered behavior.
- [ ] **I will verify freshness on follow-up passes and when fetched content matches a prior session's fetch byte-for-byte.**
- [ ] I will not fabricate citations or quotes presented as real.
- [ ] I will flag discrepancies, not hide them.
- [ ] **If the requester directly contradicts a finding, I will treat their observation as correct by default and investigate the source of my fetched view.**
- [ ] I will run the panel balance review as described in [workflow.md](./references/workflow.md) and record the tally in Appendix E.
- [ ] I will run the defensibility audit as described in [workflow.md](./references/workflow.md) (Phase 9) and record the result in Appendix F.
- [ ] I will disclose scope limits and missing inputs in the report and calibrate confidence for any issue depending on missing inputs.
- [ ] I will disclose all assumptions and inferences clearly in the methodology note.
- [ ] I will produce the report in the requested format.
