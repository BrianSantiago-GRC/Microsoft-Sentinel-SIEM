# Microsoft Sentinel SIEM Lab

A hands-on lab project where I deployed Microsoft Sentinel in Azure and worked through the full cycle of log ingestion, KQL query writing, alert creation, and incident investigation.

I built this to get comfortable with cloud-based SIEM operations before stepping into a professional environment. The goal was not to check boxes but to actually understand how log sources flow into Sentinel, how analytics rules fire, and what a Tier 1 investigation workflow looks like in practice.

---

## What I Did

**Deployed Sentinel and connected data sources**

Set up a Log Analytics workspace, enabled Sentinel, and connected Azure AD sign-in logs, Windows Security Event logs, and Defender for Cloud telemetry. Verified ingestion was working across log tables before moving to detection work.

**Wrote KQL queries for detection**

Spent most of the time here. Started with basic queries and worked up to detection logic for failed sign-ins, unusual login patterns, and Azure AD changes. A few examples:

Failed sign-in threshold:
```kql
SigninLogs
| where ResultType != 0
| summarize FailedAttempts = count() by UserPrincipalName, IPAddress
| where FailedAttempts > 5
```

Login volume by user and IP:
```kql
SigninLogs
| summarize LoginCount = count() by UserPrincipalName, IPAddress
| where LoginCount > 10
```

Azure AD administrative changes:
```kql
AuditLogs
| where OperationName contains "Add" or OperationName contains "Update"
| project TimeGenerated, InitiatedBy, TargetResources
```

**Built and tuned analytics rules**

Created custom analytics rules from the KQL queries. The tuning part was more interesting than I expected. Getting the thresholds wrong in either direction creates real problems: too sensitive and you drown in noise, too loose and you miss things.

**Triaged and investigated incidents**

Worked through the generated alerts in Sentinel's incident view. Correlated signals, followed the entity relationship graph, and documented findings the way you would in a real SOC handoff.

**Built workbooks**

Created workbooks to visualize login patterns, alert trends, and activity over time. Useful for getting a quick read on what is normal before diving into specific alerts.

---

## Tools

- Microsoft Sentinel
- Azure Log Analytics Workspace
- Azure Active Directory logs
- Microsoft Defender data sources
- Kusto Query Language (KQL)
- Azure Portal

---

## What I Took Away

The detection logic and tuning work was more nuanced than I expected. The investigation workflow made more sense once I understood how entity mapping works in Sentinel. This lab gave me a solid foundation for working with cloud SIEM environments and understanding what is happening underneath the alerts.
