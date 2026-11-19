# DET-Active Directory-004: Resource-Based Constrained Delegation Modification

## Summary

Detect modifications to the Active Directory `msDS-AllowedToActOnBehalfOfOtherIdentity` attribute, which controls which security principals may act on behalf of other identities to services running under the target account. An unauthorized change can enable resource-based constrained delegation (RBCD) abuse and impersonation.

| Attribute | Value |
|---|---|
| ID | DET-Active Directory-004 |
| Data source | Windows Security logs from domain controllers |
| Event | 5136 — A directory service object was modified |
| Attribute | `msDS-AllowedToActOnBehalfOfOtherIdentity` |
| MITRE ATT&CK | T1098 — Account Manipulation |

## Detection logic

Alert on Event 5136 when `AttributeLDAPDisplayName` equals `msDS-AllowedToActOnBehalfOfOtherIdentity`. Include both value additions and deletions. Windows commonly emits a Value Deleted event and a Value Added event for one change; correlate them by `OpCorrelationID` when available to show the before and after values without losing either individual change.

## Required telemetry

Enable Audit Directory Service Changes and configure the appropriate SACL to audit writes to this attribute on relevant computer and service account objects. Collect Event 5136 from every domain controller, including the subject account, object DN/GUID, attribute name/value, operation type, correlation ID, and timestamp. Without the matching SACL, the change may not generate Event 5136.

## Investigation

Identify the actor and modified object. Review the previous and new security descriptor values and resolve the added or removed trustee SIDs to accounts or computer objects. Confirm the change with the directory or service owner and an approved change record. Check whether the actor or target object was recently created or modified and investigate any subsequent service-ticket requests or impersonation activity. If unauthorized, follow incident procedures to remove the delegation entry with approval, contain affected accounts, and preserve evidence.

## Limitations

The attribute stores an NT security descriptor, so `AttributeValue` may be difficult to interpret without decoding and SID resolution. Event 5136 auditing requires policy and SACL configuration. Legitimate service configuration can trigger the rule; validate changes with the service owner.
