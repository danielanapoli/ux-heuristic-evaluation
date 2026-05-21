# Severity Rating Systems

Every issue gets **both** scores. Discrepancies between them are signal.

## FMEA (Soares' UX adaptation)

Score each dimension 1–10:

- **S — Severity:** How bad is the impact? (1 = trivial; 10 = task failure / harm / abandonment)
- **O — Occurrence:** How often will users encounter this? (1 = rare edge case; 10 = nearly every session)
- **D — Detection (team-side):** How hard is it for the **product team** to catch this through normal QA, testing, or analytics? (1 = obvious in any test; 10 = invisible without dedicated research)

*Note: user-side perception is captured in S and O. D reflects team-side blind spots only.*

**RPN = S × O × D** (range 1–1000).

## RPN bands (calibrate in Phase 1)

Default bands assume a transactional product. **Calibrate to product context** in Phase 1 and record the calibration in the methodology note:

- **Transactional / safety-critical:** default bands.
- **Informational / content site:** shift down ~50 points (Critical ≥150).
- **Portfolio / personal site:** shift down ~80 points (Critical ≥120).
- **Internal tool:** default or slightly down.

**Default bands:** Critical ≥200; High 100–199; Medium 50–99; Low <50.

## Nielsen Severity Ratings

- **0** — Not a usability problem
- **1** — Cosmetic; fix if time permits
- **2** — Minor; low priority
- **3** — Major; high priority
- **4** — Catastrophe; must fix before release

Show your reasoning for each dimension.

## Calibration anchors

Use these to cross-check scores before filing. If your score lands far from a comparable anchor, revisit your reasoning. Anchors assume default (transactional) bands — scale mentally if you have calibrated bands for a different product category.

Sources: Nielsen (1994), "Severity Ratings for Usability Problems," NN/g; Sauro (2013), "Prioritizing Problems in the User Experience: The FMEA," MeasuringU; MIT 6.813 Heuristic Evaluation course materials.

---

**Critical — RPN ~216 / Nielsen 4**
*Pattern:* Closing a document window with unsaved changes produces no confirmation dialog — data is silently lost. (Nielsen 1994; MIT 6.813 course materials, cited as a canonical severity-4 example.)
- S: 9 — irrecoverable data loss; high emotional and task impact.
- O: 6 — encountered by any user who closes without saving, a common workflow error.
- D: 4 — reproducible in basic functional testing but easy to miss in happy-path QA.
- Nielsen: 4 — catastrophe; must fix before release.
- *Note:* High S elevates this to Critical even when O is moderate. Irrecoverability is the driver — contrast with recoverable task failures, which score lower on S.

---

**Medium — RPN ~60 / Nielsen 3**
*Pattern:* Error messages identify that a form submission failed but do not specify which field is invalid or why. (Nielsen 1994, heuristic #9 — Help users recognize, diagnose, and recover from errors; Sauro 2013, FMEA applied to car-valuation web task.)
- S: 5 — task is recoverable but requires the user to hunt for the problem; abandonment risk on long or complex forms.
- O: 4 — encountered only when users make input errors; frequency varies with form complexity and user familiarity.
- D: 3 — reproducible in any form-submission test with invalid input.
- Nielsen: 3 — major; high priority.
- *Note:* Nielsen 3 can sit in Medium RPN when occurrence is bounded by error-prone conditions rather than universal exposure. Surface the FMEA/Nielsen discrepancy; don't flatten it.

---

**Low — RPN ~12 / Nielsen 1**
*Pattern:* Inconsistent capitalization across navigation labels (e.g., "My account" vs "My Orders" vs "settings"). (Nielsen 1994, heuristic #4 — Consistency and standards.)
- S: 2 — cosmetic; no task impact, minor cognitive friction on first encounter.
- O: 3 — visible on every visit but habituated quickly; users learn to ignore it.
- D: 2 — caught in visual QA, content audit, or any design review.
- Nielsen: 1 — cosmetic; fix if time permits.
- *Note:* Low scores across all three dimensions. If your candidate scores similarly on S and O but D is high (invisible without dedicated research), reconsider whether it belongs in Medium.
