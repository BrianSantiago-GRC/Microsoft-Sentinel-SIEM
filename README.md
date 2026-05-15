# Microsoft Sentinel SIEM Lab

Personal SIEM learning lab for practicing Microsoft Sentinel concepts, log review, basic KQL, alert logic, and security operations documentation.

This project is part of my transition from IT support into junior cybersecurity operations. It is a learning project, not production SOC ownership or advanced detection engineering.

---

## Purpose

The purpose of this lab is to practice how log data flows into Microsoft Sentinel and how a junior analyst might review alerts, document findings, and understand basic investigation steps.

---

## What I Practiced

- Setting up a Microsoft Sentinel learning environment.
- Reviewing how logs are ingested into a Log Analytics workspace.
- Writing basic KQL queries for sign-in and activity review.
- Creating simple alert concepts from query results.
- Reviewing generated incidents and documenting what was observed.
- Thinking through escalation notes and handoff quality.

---

## Tools Used

- Microsoft Sentinel
- Azure Log Analytics Workspace
- Microsoft Entra ID / Azure AD logs
- Windows Security Event logs
- Microsoft Defender data sources, where available
- Kusto Query Language (KQL)
- Azure Portal

---

## Example KQL Practice

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

Administrative activity review:

```kql
AuditLogs
| where OperationName contains "Add" or OperationName contains "Update"
| project TimeGenerated, InitiatedBy, TargetResources
```

---

## Skills Demonstrated

- SIEM learning and log review.
- Basic KQL query practice.
- Alert triage concepts.
- Microsoft identity log awareness.
- Incident note documentation.
- Operational thinking around escalation and handoff.

---

## What I Learned

This lab helped me understand how Sentinel organizes logs, alerts, entities, and incidents. The most useful lesson was that alert review is not just about seeing a signal. It is about documenting what happened, what evidence supports the finding, and what should happen next.

---

## Screenshots

Screenshots will be added as available.

Planned screenshots:

- Sentinel workspace overview.
- Log Analytics query view.
- Example query result.
- Example incident or alert view.
- Workbook or visualization, if available.

---

## Limitations

This is a personal lab. It does not represent production SOC ownership, enterprise SIEM administration, or advanced detection engineering. It is meant to show hands-on learning and documentation discipline.

---

## Next Improvement

- Add screenshots.
- Add a short incident notes example.
- Add a simple explanation of one alert review workflow.
- Connect this lab to the phishing analysis workflow project.
