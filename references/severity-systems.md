# Severity Rating Systems
 
Every issue gets **both** scores. Discrepancies between them are signal.
 
## FMEA (Soares' UX adaptation)
 
Score each dimension 1–10:
 
- **S — Severity:** How bad is the impact? (1 = trivial; 10 = task failure / harm / abandonment)
- **O — Occurrence:** How often will users encounter this? (1 = rare edge case; 10 = nearly every session)
- **D — Detection (team-side):** How hard is it for the **product team** to catch this through normal QA, testing, or analytics? (1 = obvious in any test; 10 = invisible without dedicated research). User-side perception is captured in Severity and Occurrence, not here.

**RPN = S × O × D** (range 1–1000).
 
## RPN bands (calibrate in Phase 1)
 
Default bands assume a transactional product. **Calibrate to product context** in Phase 1 and record the calibration in the methodology note:
 
- **Transactional / safety-critical:** default bands.
- **Informational / content site:** shift down ~50 points (Critical ≥150).
- **Portfolio / personal site:** shift down ~80 points (Critical ≥120).
- **Internal tool:** default or slightly down.

**Default bands:** Critical ≥200; High 100–199; Medium 50–99; Low <50.
 
##  Nielsen Severity Ratings
 
- **0** — Not a usability problem
- **1** — Cosmetic; fix if time permits
- **2** — Minor; low priority
- **3** — Major; high priority
- **4** — Catastrophe; must fix before release

Show your reasoning for each dimension.
