deviceEventClassId IN (4728, 4732, 4756)
AND destinationGroupName IN (
  "Domain Admins",
  "Enterprise Admins",
  "Schema Admins",
  "Administrators",
  "Backup Operators",
  "Account Operators"
)
AND NOT InActiveList("sourceUserWL")
AND NOT InActiveList("targetUserWL")
AND NOT InActiveList("targetGroupWL")
