# Per-Issue Report Schema
 
```markdown
## Issue [#]: [Short, action-oriented title]
 
**Type:** Heuristic Violation | Quality Issue
 
**Location:** [Screen / component / URL / step in flow]
 
**Steps to reproduce:**
1. ...
2. ...
3. ...
 
**Observed behavior:** [What happens]
**Expected behavior:** [What a well-designed alternative would do]
 
**Violated heuristic(s):** *(Heuristic Violation only)*
- Nielsen #X — [name]
- Shneiderman #X — [name]
 
**Rationale for mapping:** *(Heuristic Violation only)*
 
**Why it matters:** *(Quality Issue only)*
 
**Expert perspectives:**
- **[Expert name]:** *"[Simulated quote]"* — [lens contribution]
- [2–4 total. Note any disagreement.]
 
**Severity — FMEA (Soares):**
- S: X — [why]
- O: X — [why]
- D: X — [why — team-side detectability]
- **RPN: X** ([band per the calibration set in Phase 1])
 
**Severity — Nielsen:** X — [why]
 
**Discrepancy flags:** [FMEA-vs-Nielsen tension or inter-expert disagreement]
 
**Verification status:** Rendered browser ✓ / HEAD request ✓ / Static-only — limit noted / N/A. **For follow-up passes:** freshness verified via [method] on [timestamp].
 
**Prevalence / context:** Novel / Common / Well-documented anti-pattern. Real citation or "expert judgment only."
 
**Recommendation:**
- **Primary fix:** [one concrete change]
- **Stretch fix:** [optional deeper change]
```
 
## Final Report Structure
 
1. **Executive Summary** (≤ 1 page)
   - Scope, method, panelists, date, product-category calibration applied
   - **Top themes (3–5):** patterns *across* issues — not individual issues.
   - **Top issues by RPN (3):** highest-RPN single items, one line each. Must not duplicate themes.
   - **Recommended next steps:** immediate / near-term / strategic.
2. **Issue Catalog** — sorted by RPN, descending. Heuristic Violations and Quality Issues both live here, tagged by `Type`.
3. **Patterns & Themes**
4. **Methodology Note**
   - Frameworks (Nielsen, Shneiderman)
   - Severity systems (FMEA per Soares; Nielsen severity)
   - Calibration applied to RPN bands
   - Simulated expert panel disclaimer
   - **Freshness verification method used** (for follow-up passes)
   - Limitations of automated evaluation
   - Inputs not available
5. **Appendices**
   - A. Heuristic reference
   - B. Severity scoring rubric with calibration used
   - C. Design observations
   - D. Issues considered and excluded
   - E. Panel balance tally
   - F. Defensibility audit result — Phase 9 check with pass/fail per point

## Tone & Voice
 
- Direct, specific, and respectful of the design team's work.
- Critique the artifact, not the people.
- Concrete language over vague.
- One primary fix per issue.
