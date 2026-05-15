# Incident Notes Example

## Incident Type

Repeated failed authentication activity observed in a Sentinel honeypot lab.

## Severity

Low to medium in the lab context.

In a production environment, severity would depend on:

- target account sensitivity
- successful login evidence
- affected host exposure
- source reputation
- business impact

## Summary

Failed Windows logon activity was reviewed in Microsoft Sentinel / Log Analytics using basic KQL queries. The activity was analyzed by source, account, and time window to understand whether repeated authentication failures could indicate brute force behavior or unauthorized access attempts.

## Evidence Reviewed

- Windows Security Event ID 4625 for failed logons.
- Failed logon counts by source IP.
- Failed logon counts by account.
- Time-based distribution of events.
- Presence or absence of related successful logons.

## Findings

- Failed authentication activity can be summarized quickly with basic KQL.
- Repeated failures become more useful when grouped by source, account, and time window.
- Failed logons alone are not enough to prove compromise.
- Clear documentation should separate observed facts from assumptions.

## Recommended Follow-Up

For a real environment, recommended follow-up would include:

- Confirm whether the exposed service should be publicly reachable.
- Review whether MFA is enabled for affected accounts.
- Check for successful logons after repeated failures.
- Validate account lockout and password policies.
- Review firewall, NSG, or conditional access controls.
- Escalate to a senior analyst if successful access or sensitive account targeting is found.

## Limitations

Screenshots and raw exported logs were not captured during the original lab. This incident note is a portfolio documentation artifact based on the completed lab workflow.
