# Follow-up / Delta Pass Protocol

Applies whenever the requester says any variant of "I've made changes" or "can you re-evaluate."

The dominant risk is **silently evaluating stale data**: the fetch tool returns a pre-change cached version, and the agent files findings claiming issues persist when they've been resolved.

## Step 1 — Establish a freshness fingerprint before fetching

Ask the requester (or check the site) for one of:

- Deploy date of the changes.
- A visible "Last updated" stamp, build hash, or version string.
- A specific element that changed — a label, nav item, removed section — that can serve as proof of freshness.

Write the fingerprint into scratch notes before any fetch.

## Step 2 — Fetch and validate against the fingerprint

After fetching, check the fingerprint immediately. If it doesn't match, the fetch is stale — **stop. Do not file any findings until freshness is confirmed.**

**Freshness verification methods, in order:**
1. Render in a real browser (e.g., Claude in Chrome) — bypasses caches, exercises real DOM.
2. Append a cache-busting query parameter (e.g., `?nocache={timestamp}`).
3. Compare on-page recency signals against the requester's reported change date.
4. Ask the requester to confirm one specific element as a freshness fingerprint.

Full rationale and escalation guidance in [workflow.md](./workflow.md) — Verification escalation (freshness).

## Step 3 — Compare against the prior evaluation

For each prior issue, classify as:

- **Resolved** — fix visible in fresh fetch.
- **Partially resolved** — some instances fixed, others not. Note which.
- **Unchanged** — persists. Re-verify per Phase 2's rendered-behavior rule before re-filing.
- **Regressed** — fix introduced a new problem. File as a new issue.

## Step 4 — Scan for new issues introduced by the changes

Walk changed pages once more after classifying prior issues.

## Step 5 — Conflict resolution and disclosure

If your fetch shows an issue persisting but the requester says it's fixed: default to the requester per the Defensibility Rules in SKILL.md. Investigate before filing — refetch with cache-busting, render in a real browser, or ask the requester to confirm a specific element. Do not publish a delta report that contradicts the requester without resolving the conflict.

The delta report's methodology note must state: that this was a follow-up pass; the freshness fingerprint used and how it was verified; the fetch method and its known cache limitations; any conflicts and how they were resolved. See [report-guidelines.md](./report-guidelines.md) for the full Methodology Note structure.