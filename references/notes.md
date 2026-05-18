# General notes 

## Future improvements
 
The four methods for verifying freshness (rendered browser → cache-busting URL → on-page recency signal → requester confirmation) — defined in [workflow.md](./workflow.md), Verification escalation — freshness — currently treat browser-rendering as one option among several. A **heavier-handed alternative** would make rendered-browser fetching (e.g., Claude in Chrome) the **default** for all follow-up passes, with static `WebFetch` reserved only for cases where rendering isn't available. That would close the stale-content failure mode at the tool level rather than relying on the agent to apply the escalation rules correctly each time.
 
This version of the protocol intentionally stops short of that for two reasons: (1) rendered-browser fetching is slower and more expensive than `WebFetch`, and (2) requester-confirmation gives the requester useful visibility into what the agent is checking and a chance to correct course early. If stale-content failures recur despite the [Follow-up Protocol](./follow-up-protocol.md) being applied, revisit this trade-off — promoting rendered-browser to the default is a one-line change in Step 2 of that protocol and in the freshness escalation methods in [workflow.md](./workflow.md).
