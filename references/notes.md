# General notes

## Future improvements

The four methods for verifying freshness (rendered browser → cache-busting URL → on-page recency signal → requester confirmation) — defined in [workflow.md](./workflow.md), Verification escalation — freshness — currently treat browser-rendering as one option among several. A **heavier-handed alternative** would make rendered-browser fetching (e.g., Claude in Chrome) the **default** for all follow-up passes, with static `WebFetch` reserved only for cases where rendering isn't available. That would close the stale-content failure mode at the tool level rather than relying on the agent to apply the escalation rules correctly each time.

This version of the protocol intentionally stops short of that for two reasons: (1) rendered-browser fetching is slower and more expensive than `WebFetch`, and (2) requester-confirmation gives the requester useful visibility into what the agent is checking and a chance to correct course early. If stale-content failures recur despite the [Follow-up Protocol](./follow-up-protocol.md) being applied, revisit this trade-off — promoting rendered-browser to the default is a one-line change in Step 2 of that protocol and in the freshness escalation methods in [workflow.md](./workflow.md).

Calibration anchors in [severity-systems.md](./severity-systems.md) are currently grounded in foundational literature (Nielsen 1994, Sauro 2013). As real evaluations accumulate, consider replacing or supplementing these with validated findings from your own work — anchors drawn from first-hand scored issues will be more precisely calibrated to your product categories and evaluation style.

---

## Changelog

### May 20, 2026

First optimization and integrity pass. Files changed: SKILL.md, workflow.md, follow-up-protocol.md, expert-lenses.md, report-guidelines.md, severity-systems.md. frameworks.md unchanged.

**Token optimization**

The primary goal was reducing token cost without degrading output quality. Key changes:

- *SKILL.md:* Collapsed the Kickoff Checklist from 17 items to 10 by removing items that directly restated Defensibility Rules or Instructions. Cut preamble sentences throughout. Net: −11 lines.
- *workflow.md:* Compressed phase descriptions to imperative fragments. Removed a redundant example from the freshness fingerprint trigger list. Net: −11 lines.
- *follow-up-protocol.md:* Collapsed Steps 5 and 6 (conflict resolution and disclosure) into a single step with a pointer to the canonical Defensibility Rule in SKILL.md and the Methodology Note structure in report-guidelines.md. Replaced the inline freshness method list with a pointer to workflow.md, then reinstated the list (see Integrity section below). Net: −7 lines.
- *expert-lenses.md:* Dropped the "What it brings" column from the Panel Clusters table — content was redundant with the "Core lens" column in the main expert table above it. Net: same line count, fewer tokens.
- *report-guidelines.md:* Cut two of four Tone & Voice bullets ("Direct, specific" and "Concrete language over vague") as generic writing guidance Claude applies without instruction. Added fetch method to Methodology Note disclosure list. Net: −2 lines.

Estimated total token saving vs. original: ~600–900 tokens per full invocation (~20–25% of total skill footprint).

**Integrity improvements**

Six risks to output validity, soundness, defensibility, and expert-led nature were identified and addressed:

1. *Required inputs gate (SKILL.md):* Added ⛔ hard-stop before the inputs list. Split inputs into blocking (artifact, primary user, top tasks — no fallback) and non-blocking (all others). Tightened the fallback clause to apply only after asking, closing the loophole that allowed silent inference as a substitute for asking. *Impact:* Evaluations now cannot begin without the three inputs that define the evaluation's frame of reference — primary user and task context are no longer optional. Validity strengthened.

2. *Freshness protection (SKILL.md + follow-up-protocol.md):* Added a dedicated freshness checklist item to SKILL.md with the four verification methods inline, and a hard stop in Step 2 of follow-up-protocol.md ("Do not file any findings until freshness is confirmed") with the method list also inline. The pointer to workflow.md for full rationale is preserved. *Impact:* Freshness is now defended at two independent points — SKILL.md catches skipped protocol reads; Step 2 catches skipped chain-following. Defensibility of follow-up passes strengthened.

3. *Fetch method disclosure (SKILL.md + workflow.md):* Added a checklist item requiring the fetch method (rendered browser or static) to be noted before starting, with static fetch triggering a mandatory Methodology Note disclosure. Added as Phase 9 audit item #12. *Impact:* Previously invisible methodological choice is now visible and auditable in every report. Defensibility strengthened.

4. *Phase ordering enforcement (workflow.md):* Added an explicit warning at the top of workflow.md: severity scoring (Phase 5) must not precede expert reconciliation (Phase 4); executive summary must not precede full issue cataloging. The two most tempting shortcuts are named explicitly. *Impact:* Expert perspectives now reliably inform severity scores rather than being applied post-hoc. Expert-led nature and soundness strengthened.

5. *Bucket assignment challenge (workflow.md, Phase 3):* Added a forcing question before any Heuristic Violation filing: state which specific heuristic is violated and what observable behavior causes it — in one sentence. Failure to answer reassigns to Quality Issue. *Impact:* Reduces inflated Heuristic Violation counts, a known validity problem in expert reviews. Validity and soundness strengthened.

6. *Panel balance tally (workflow.md, Phase 7):* Replaced the vague "record the tally in Appendix E" instruction with a required structured table (cluster / members cited / citation count / % of total / threshold met). Added to Phase 9 audit item #8. *Impact:* Panel balance shifts from a declared outcome to a documented and auditable one. Expert-led nature and defensibility strengthened.

7. *Severity calibration anchors (severity-systems.md):* Replaced three synthetic anchor examples with patterns grounded in published literature: unsaved data loss on window close (Nielsen 1994 / MIT 6.813, Critical / Nielsen 4), uninformative error messages (Nielsen heuristic #9 / Sauro 2013 MeasuringU, Medium / Nielsen 3), and inconsistent navigation capitalization (Nielsen heuristic #4, Low / Nielsen 1). All sources cited inline. *Impact:* Severity scoring now cross-references validated, attributable benchmarks rather than constructed examples. Soundness and defensibility strengthened; evaluator effect (Hertzum et al. 2002) partially mitigated by providing shared reference points.