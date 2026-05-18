# Follow-up / Delta Pass Protocol
 
A follow-up pass — an evaluation that runs after the requester reports changes have been made — has a different failure profile than a first pass. The dominant risk is **silently evaluating stale data**: the fetch tool returns the pre-change version of the page (from its own cache, a CDN edge, or upstream HTTP caching), and the agent files findings claiming issues persist when in fact they have been resolved.
 
This protocol applies whenever the requester says any variant of "I've made changes" or "can you re-evaluate."
 
## Step 1 — Establish a freshness fingerprint before fetching
 
Ask the requester (or look on the site itself) for one of:
 
- The deploy date of the changes.
- A visible "Last updated" stamp, build hash, or version string.
- A specific element they know changed — a label, a nav item, a removed section — that you can check for as proof of freshness.

Write the fingerprint into your scratch notes before any fetch.
 
## Step 2 — Fetch and validate against the fingerprint
 
After fetching, **check the fingerprint immediately**:
 
- If a "Last updated" date is older than the requester's reported deploy date → fetch is stale. Escalate per the freshness rules in [workflow.md](./workflow.md) (Verification escalation — freshness).
- If the changed element looks unchanged in the fetched content → fetch is stale. Escalate.
- If the fingerprint matches → proceed with the delta.

## Step 3 — Compare against the prior evaluation
 
For each issue from the prior evaluation, classify as one of:
 
- **Resolved** — the fix is visible in the fresh fetch.
- **Partially resolved** — some pages or instances fixed, others not. Note which.
- **Unchanged** — the issue persists. Re-verify per Phase 2's rendered-behavior rule before re-filing.
- **Regressed or newly worsened** — the fix introduced a new problem (e.g., the partial fix created a new inconsistency). File as a new issue.

## Step 4 — Scan for new issues introduced by the changes
 
A change rarely fixes only what it targets. After classifying prior issues, walk the changed pages once more looking for new candidates.
 
## Step 5 — Conflict resolution
 
If the requester reports the issue is fixed and your fetched content shows it persisting:
 
- **Default to the requester's observation.**
- Investigate the source of the discrepancy before filing anything: refetch with cache-busting, render in a real browser, ask for a screenshot, or ask the requester to confirm a specific element in DevTools.
- Do not publish a delta report that contradicts the requester without resolving the conflict.

## Step 6 — Disclose in the report
 
The delta report's methodology note must state:
 
- That this was a follow-up pass.
- The freshness fingerprint used and how it was verified.
- The tool/method used for fetching (and its known cache limitations).
- Any conflicts with requester observation and how they were resolved.
