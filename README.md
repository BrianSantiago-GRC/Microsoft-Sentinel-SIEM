# Microsoft Sentinel Honeypot SIEM Lab

Completed portfolio write-up for a Microsoft Sentinel honeypot lab.

This project documents a completed hands-on lab where a honeypot-style Windows endpoint was used to practice Microsoft Sentinel log ingestion, failed sign-in review, basic KQL, alert triage thinking, and incident documentation.

This is a junior cybersecurity portfolio project. It does not claim SOC ownership, Sentinel administration ownership, production monitoring, detection engineering, or threat hunting experience.

---

## Project Purpose

The purpose of this lab was to understand how suspicious authentication activity can be collected, reviewed, and documented in Microsoft Sentinel.

The lab focuses on practical security operations skills:

- Reviewing failed authentication activity.
- Using KQL to filter and summarize security events.
- Building an analyst timeline from observed activity.
- Writing clear incident notes.
- Explaining what evidence was available and what was missing.
- Connecting IT troubleshooting skills to junior SOC investigation work.

---

## Lab Scope

This project is based on a completed honeypot/Sentinel lab. Screenshots were not captured during the original lab, so this repository uses written evidence, KQL examples, and analyst documentation instead of fake images.

No live tenant IDs, public IP addresses, usernames, device names, or private environment details are included.

---

## Tools Used

- Microsoft Sentinel
- Azure Log Analytics Workspace
- Windows Security Events
- Kusto Query Language (KQL)
- Azure Portal
- Windows virtual machine / honeypot-style endpoint
- Markdown documentation

---

## What I Practiced

- Connecting security event data into a Sentinel / Log Analytics workflow.
- Reviewing failed login activity from a Windows endpoint.
- Writing basic KQL to filter authentication events.
- Summarizing source activity by account, IP, and time window.
- Thinking through alert triage from a junior analyst perspective.
- Documenting findings, limitations, and recommended follow-up.

---

## Evidence and Documentation

| Artifact | Purpose |
|---|---|
| [Lab Summary](evidence/honeypot-lab-summary.md) | Documents the completed lab scope and what was practiced. |
| [KQL Queries](evidence/kql-queries.md) | Shows the query patterns used for failed authentication and event review. |
| [Analyst Timeline](evidence/analyst-timeline.md) | Shows how the investigation was organized chronologically. |
| [Incident Notes](evidence/incident-notes.md) | Provides a junior SOC-style incident note example. |
| [Lessons Learned](evidence/lessons-learned.md) | Captures what the lab reinforced and what to improve next. |
| [Screenshot Status](screenshots/README.md) | Explains why screenshots are not included and what would be captured in a future recreation. |

---

## KQL Practice Examples

Failed Windows logon review:

```kql
SecurityEvent
| where EventID == 4625
| project TimeGenerated, Computer, Account, IpAddress, Activity
| order by TimeGenerated desc
```

Failed logons by source IP:

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedLogons = count() by IpAddress
| order by FailedLogons desc
```

Failed logons over time:

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedLogons = count() by bin(TimeGenerated, 1h)
| order by TimeGenerated asc
```

Account activity review:

```kql
SecurityEvent
| where EventID in (4624, 4625)
| summarize EventCount = count() by Account, EventID
| order by EventCount desc
```

---

## Skills Demonstrated

- SIEM fundamentals.
- Microsoft Sentinel workflow awareness.
- Windows authentication event review.
- Basic KQL query writing.
- Failed logon analysis.
- Alert triage thinking.
- Incident note documentation.
- Evidence limitation handling.
- Junior SOC communication.

---

## Interview Talking Point

"I completed a Microsoft Sentinel honeypot lab to practice reviewing failed authentication activity from a Windows endpoint. I used Sentinel and Log Analytics to understand how security events can be queried with KQL, summarized by source and time window, and documented in a junior analyst-style incident note. I did not capture screenshots during the original lab, so I documented the workflow, queries, timeline, and lessons learned instead of inventing evidence."

---

## Lessons Learned

This lab reinforced that SIEM work is not just about seeing logs. A useful analyst needs to explain:

- What activity was observed.
- Which events supported the finding.
- What was suspicious or worth reviewing.
- What evidence was missing.
- What should happen next.

The most useful part of the lab was practicing how to turn raw failed-login activity into clear notes that another analyst or manager could understand.

---

## Screenshot Status

Screenshots are not included because they were not captured during the completed lab.

This project will not use fake screenshots. If the lab is recreated later, screenshots should be added only after sensitive data is removed.

Planned future screenshots:

- Sentinel workspace overview.
- Log Analytics query view.
- Failed logon query result.
- Incident or alert view if configured.
- Workbook or map visualization if rebuilt.

---

## Future Improvements

- Recreate the lab and capture sanitized screenshots.
- Add a small workbook visualization if available.
- Add one completed alert rule example.
- Add a phishing-to-Sentinel connection scenario.

---

## Limitations

This was a personal lab and portfolio project. It does not represent production SOC monitoring, enterprise SIEM administration, advanced threat hunting, or detection engineering.
