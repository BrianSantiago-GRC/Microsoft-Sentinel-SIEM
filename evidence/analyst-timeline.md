# Analyst Timeline Walkthrough

This is a written timeline format for explaining the completed honeypot lab in an interview.

## Timeline

| Step | Analyst Action | Purpose |
|---|---|---|
| 1 | Confirmed the lab objective | Practice Sentinel log review and failed authentication analysis. |
| 2 | Reviewed Windows security event context | Focused on failed authentication events and basic endpoint evidence. |
| 3 | Queried failed logon activity | Used KQL to filter for failed Windows logon events. |
| 4 | Summarized activity by source and account | Looked for repeated attempts, concentration by source, and account targeting. |
| 5 | Reviewed time window patterns | Checked whether activity appeared isolated or repeated over time. |
| 6 | Documented findings | Wrote clear notes about what was observed and what evidence was missing. |
| 7 | Recommended follow-up | Focused on containment and hardening steps appropriate for a junior analyst recommendation. |

## Investigation Logic

The investigation was organized around basic SOC triage questions:

- What happened?
- Which host or account was involved?
- What event IDs support the finding?
- How many failures occurred?
- Was there evidence of successful access?
- What should be reviewed next?

## Escalation Criteria

Activity would be worth escalating if:

- repeated failures targeted the same account
- repeated failures came from the same source
- failed logons were followed by a successful logon
- activity matched an exposed service or weak access control
- the affected system had sensitive access or business impact

## Documentation Goal

The goal was to write notes that another analyst could follow without needing to re-run every query from scratch.
