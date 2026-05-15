# KQL Queries

These are basic KQL query patterns used for the Microsoft Sentinel honeypot lab.

Field names can vary depending on the connector and table configuration. These examples are written for junior-level review and may need small adjustments in a live workspace.

## Failed Windows Logons

```kql
SecurityEvent
| where EventID == 4625
| project TimeGenerated, Computer, Account, IpAddress, Activity
| order by TimeGenerated desc
```

## Failed Logons By Source IP

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedLogons = count() by IpAddress
| order by FailedLogons desc
```

## Failed Logons Over Time

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedLogons = count() by bin(TimeGenerated, 1h)
| order by TimeGenerated asc
```

## Account Review

```kql
SecurityEvent
| where EventID in (4624, 4625)
| summarize EventCount = count() by Account, EventID
| order by EventCount desc
```

## Possible Brute Force Pattern

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedAttempts = count(), FirstSeen = min(TimeGenerated), LastSeen = max(TimeGenerated) by Account, IpAddress
| where FailedAttempts >= 10
| order by FailedAttempts desc
```

## Analyst Notes

Useful questions while reviewing the results:

- Is one source generating repeated failures?
- Is one account being targeted repeatedly?
- Are failures clustered in a short time window?
- Are there successful logons after repeated failures?
- Is there enough evidence to escalate, or is more context needed?
