# DET-Active Directory-001: Privileged Group Membership Modification

## Summary

Detect each successful addition of an account to a monitored privileged Active Directory group. Generate one alert for every qualifying event unless the source account, target account, **or** target group matches its corresponding independently maintained allowlist. Any single allowlist match suppresses the event; allowlist matches are combined with OR semantics.

| Attribute | Value |
|---|---|
| ID | DET-Active Directory-001 |
| Severity | High (starting point; tune to local risk model) |
| Data source | Windows Security auditing on domain controllers |
| Event IDs | 4728, 4732, 4756 |
| MITRE ATT&CK | T1098.007 — Additional Local or Domain Groups |
| Frequency | Every qualifying occurrence; no threshold or suppression window |

## Objective and scope

Identify additions to these six groups, regardless of whether the group is domain-global, domain-local, or universal:

- Domain Admins
- Enterprise Admins
- Schema Admins
- Administrators
- Backup Operators
- Account Operators

Event 4728 records addition to a security-enabled global group; 4732 to a security-enabled local group; and 4756 to a security-enabled universal group. This detection covers additions only. Removals, distribution groups, and changes that do not produce these audited events are out of scope.

## Required telemetry

Collect successful Security audit events from every domain controller, preserving the event identifier and original event data. Required fields are event ID, subject account, member account, target group, target domain, computer, and timestamp. Windows commonly records the acting account in `SubjectUserName` / `SubjectDomainName`, the added member in `MemberName`, and the receiving group in `TargetUserName` / `TargetDomainName`.

## Vendor-neutral logic

For each event, evaluate:

1. Event ID is 4728, 4732, or 4756.
2. Target group is one of the six monitored groups (case-insensitive comparison; include the domain-qualified group identity where available to avoid same-name ambiguity).
3. No independent allowlist matches:
   - source account equals an entry in the source-account list; **OR**
   - normalized target account equals an entry in the target-account list; **OR**
   - target group identity equals an entry in the target-group list.
4. Alert once for every event meeting steps 1–3. Do not aggregate or suppress repeated occurrences.

The three allowlists are separate data sets and independently managed. A match in any one is sufficient to suppress; a match in none is required to alert. Keep entries narrowly scoped, reviewed, and auditable. Empty lists suppress nothing.

## Target-account normalization

`MemberName` may be a distinguished name, a SID, or an account name. Normalize it before allowlist comparison: prefer a stable directory object SID or canonical `DOMAIN\account` identity obtained from trusted enrichment. If only a DN is available, resolve the DN to that canonical identity. Do not compare only the first CN component: it is not guaranteed unique. If resolution fails, retain the raw value, do not treat it as allowlisted, and include the resolution status in the alert.

## Alert fields

Include event timestamp, event ID, domain controller, source account and domain, target account raw and normalized identities, target group and domain, record ID, and allowlist evaluation outcome. Preserve source event details for investigation.

## False positives and limitations

Legitimate identity lifecycle automation, approved administrator changes, and recovery operations can trigger alerts. Use the relevant independent allowlist only when the activity is predictable and tightly bounded; allowlisting an entire group suppresses all membership additions to it. Missing audit policy, incomplete domain-controller collection, parsing failures, and unresolved member identities can reduce fidelity. Event IDs and field names can vary in representation by collector; validate mappings in the deployed pipeline.

## Response

Confirm the change with the directory owner and approved change record. Verify the actor, added identity, group, domain controller, and exact event time; determine whether the actor's session and source host are expected. Review nearby authentication, privilege use, and subsequent group changes. If unauthorized, follow incident procedures to contain the account/session, remove the unauthorized membership with authorization, preserve evidence, and assess actions performed while privileged.

## Implementation notes

The Elastic KQL file is the base event-and-group filter. KQL does not query arbitrary external lists. Apply the three allowlists as three independent Elastic Security rule exception conditions (one condition per dimension), configured so a match in any exception suppresses the alert. The ArcSight condition specification is maintained separately under `detections/arcsight/`. Verify platform-specific exception behavior, account normalization/enrichment, and field mappings in the deployed SIEM.
