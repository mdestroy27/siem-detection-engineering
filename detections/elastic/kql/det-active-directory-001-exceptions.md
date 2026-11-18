# Elastic exception configuration: DET-Active Directory-001

The KQL rule includes the current whitelist values as three independent `not field: value` conditions. KQL does not read the JSON whitelist file automatically, so update the corresponding KQL clause whenever its independently maintained list changes. Alternatively, configure three independent rule exception entries in Elastic Security, each as a single-value exact match against the corresponding field. A match to any exception entry excludes the event; verify the deployed Elastic version's behavior before production use.

| Independent list | Exception field | Example value |
|---|---|---|
| Source accounts | `winlog.event_data.SubjectUserName` | `svc_identity_sync` |
| Target accounts | `ad.member.canonical` (enriched stable identity; see specification) | `EXAMPLE\breakglass` |
| Target groups | `winlog.event_data.TargetUserName` | `Domain Admins` |

Do not put all values in a single multi-field exception: the required policy is that a match in any one dimension suppresses. The target-account enrichment field is a recommended normalized field and must be populated by the ingest pipeline. An unresolved raw DN must not accidentally match a short account name. Empty lists have no exception entries and therefore suppress nothing.
