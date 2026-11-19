# DET-Active Directory-002: Successful Authentication After Repeated Failures

## Summary

Detect a successful Windows authentication that follows repeated failed attempts for the same account from the same source to the same host. This may indicate password guessing or password spraying followed by a successful login.

| Attribute | Value |
|---|---|
| ID | DET-Active Directory-002 |
| Data source | Windows Security logs |
| Events | 4625 (failed logon), followed by 4624 (successful logon) |
| Initial condition | At least 5 failures followed by a success within 10 minutes |
| MITRE ATT&CK | T1110 — Brute Force |

## Detection logic

Correlate events by normalized target account, source IP, and destination host:

1. Observe at least five Event 4625 failures for the same account/source/host.
2. Within 10 minutes of the first failure, observe an Event 4624 success with the same correlation values.
3. Generate an alert containing the failures and successful login details.

Five failures in ten minutes is an initial tuning value. Adjust it to local authentication patterns. Require a source IP and target account for reliable correlation; treat missing values separately rather than joining unrelated events.

## Required fields

Event ID, timestamp, target account and domain, source IP, destination host, logon type, authentication package, and outcome. Windows Event 4624 is recorded on the computer where the session is created; Event 4625 is recorded where the attempted logon failed. Preserve the original event data and normalize the target account consistently across both event types.

## Investigation

Review the number and timing of failures, account, source IP, destination host, logon type, and authentication package. Determine whether the source and successful login are expected. Check for activity against other accounts from the same source and for later privileged actions. If suspicious, follow incident procedures to contain the account/session, investigate the source, and preserve the related authentication events.

## Limitations

Distributed attempts, missing source IPs, account normalization differences, and log collection gaps can prevent correlation. A successful login after failures can also result from mistyped passwords or legitimate user activity. Tune thresholds and exclusions against the environment.
