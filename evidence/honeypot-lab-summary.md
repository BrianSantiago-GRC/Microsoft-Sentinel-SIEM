# Honeypot Lab Summary

## Purpose

This lab was completed to practice how Microsoft Sentinel can be used to review suspicious authentication activity from a honeypot-style Windows endpoint.

The goal was not to build an enterprise SOC. The goal was to understand the basic workflow:

1. Generate or observe authentication activity.
2. Ingest security events into Log Analytics / Sentinel.
3. Query failed logon activity.
4. Review source patterns.
5. Document findings and limitations.
6. Recommend follow-up actions.

## Scope

The lab focused on failed Windows authentication activity, basic event review, KQL practice, and analyst documentation.

The lab did not include:

- production monitoring
- advanced detection engineering
- malware analysis
- threat hunting ownership
- enterprise SIEM administration

## What Was Practiced

- Reviewing Windows failed logon activity.
- Filtering events by Event ID.
- Summarizing failed attempts by source and time window.
- Thinking through when activity should be escalated.
- Writing incident notes in a clear, operational format.

## Evidence Limitation

Screenshots were not captured during the original lab. This repository documents the lab through written artifacts and KQL examples instead of fake images.

If the lab is recreated later, screenshots can be added after sensitive values are sanitized.
