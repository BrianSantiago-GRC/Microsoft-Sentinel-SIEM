# Microsoft Sentinel SIEM Lab

Personal SIEM learning lab for practicing Microsoft Sentinel concepts, log review, basic KQL, alert logic, and security operations documentation.

This project supports my transition from IT support into junior cybersecurity operations. It is a portfolio lab and does not claim SOC ownership, Sentinel administration ownership, or advanced detection work.

---

## Project Purpose

The purpose of this lab is to practice how log data flows into Microsoft Sentinel and how a junior analyst might review alerts, document findings, and understand basic investigation steps.

The project is designed to show practical learning, clear documentation, and operational reasoning.

---

## Tools Used

- Microsoft Sentinel
- Azure Log Analytics Workspace
- Microsoft Entra ID / Azure AD logs
- Windows Security Event logs
- Microsoft Defender data sources, where available
- Kusto Query Language (KQL)
- Azure Portal
- Markdown documentation

---

## What I Practiced

- Setting up a Microsoft Sentinel learning environment.
- Reviewing how logs are ingested into a Log Analytics workspace.
- Writing basic KQL queries for sign-in and activity review.
- Reviewing simple alert concepts from query results.
- Thinking through incident notes and escalation quality.
- Documenting limitations and evidence gaps clearly.

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

## Lessons Learned

This lab helped me understand how Sentinel organizes logs, alerts, entities, and incidents.

The most useful lesson was that alert review is not just about seeing a signal. It is about documenting what happened, what evidence supports the finding, and what should happen next.

---

## Screenshots / Evidence

Screenshots will be added after they are captured from the lab environment.

Current screenshot checklist:

- Sentinel workspace overview.
- Log Analytics query view.
- Example query result.
- Example incident or alert view.
- Workbook or visualization, if available.

Supporting folders:

- [screenshots/README.md](screenshots/README.md)
- [evidence/README.md](evidence/README.md)

No screenshots or incident evidence are claimed until files are added to this repository.

---

## Future Improvements

- Add sanitized screenshots.
- Add a short incident notes example.
- Add a simple explanation of one alert review workflow.
- Connect this lab to the phishing analysis workflow project.

---

## Limitations

This is a personal lab. It does not represent responsibility for a live SOC, SIEM administration role, production monitoring, or specialized detection work.
