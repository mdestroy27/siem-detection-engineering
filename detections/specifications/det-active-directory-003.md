# DET-Active Directory-003: Abnormal Kerberos Service Ticket Activity

## Summary

Detect a burst of Kerberos service ticket requests from one account for many distinct services, with emphasis on RC4-encrypted tickets. This behavior can indicate Kerberoasting.

| Attribute | Value |
|---|---|
| ID | DET-Active Directory-003 |
| Data source | Windows Security logs from domain controllers |
| Event | 4769 — A Kerberos service ticket was requested |
| Initial threshold | 10 distinct service names per requesting account and source IP within 5 minutes |
| MITRE ATT&CK | T1558.003 — Kerberoasting |

## Detection logic

Filter for Event 4769 with ticket encryption type `0x17` (RC4). Group by requesting account and client address. Alert when the group has at least 10 distinct requested service names in a rolling 5-minute window.

The threshold is a starting value. Review normal service-ticket patterns and legacy RC4 use before tuning it. RC4 alone is not proof of an attack; legitimate legacy systems can use it. A low-rate or AES-based Kerberoasting attempt may not match this rule.

## Required fields

Event ID, timestamp, requesting account, requested service name, ticket encryption type, client address, and domain controller. Windows Event 4769 is generated on domain controllers for Kerberos service-ticket requests. Preserve raw event fields for investigation.

## Investigation

Review the requester, source address, requested service names, encryption type, and timing. Determine whether the account and source normally request those services. Check the targeted service accounts for privilege and credential hygiene. Correlate with endpoint process telemetry for SPN enumeration or ticket-request tools. Escalate and respond according to incident procedures if unauthorized.

## Limitations

Event 4769 is high-volume routine telemetry. Legacy applications may use RC4, and an attacker can request tickets slowly or use AES. Tune the threshold against environment baselines and enrich the alert with service-account context where available.
