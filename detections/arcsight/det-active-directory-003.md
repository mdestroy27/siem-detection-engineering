deviceEventClassId = 4769
AND TicketEncryptionType = "0x17"

Rule threshold:
Group by requesting account + client address.
Alert on 10 or more distinct ServiceName values within 5 minutes.
