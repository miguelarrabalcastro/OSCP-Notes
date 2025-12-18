
- Sacar subdominios
```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt -u 'http://planning.htb/' -H 'Host: FUZZ.planning.htb' -fs 178

wfuzz -c -w /usr/share/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt -u http://10.13.38.11/FUZZ --hc 404 -t 100
```

- Directorio
```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://10.129.1.15/FUZZ -e .php,.txt,.html,.bak,.zip,.env,.git
```

- Usuarios
```bash
ffuf -u 'http://nocturnal.htb/view.php?username=FUZZ&file=*.pdf' -w
/usr/share/seclists/Usernames/xato-net-10-million-usernames.txt -mc 200 -fr
"User not found." -H "Cookie: PHPSESSID=4d9uqe8ifkefg1pkgu5ksi06qs
```

- Extensiones de archivos
```bash
asp
aspx
phar
php
php3
php4
php5
txt
shtm
shtml
phtm
phtml
jhtml
pl
jsp
cfm
cfml
py
rb
cfg
zip
pdf
gz
tar
tar.gz
tgz
doc
docx
xls
xlsx
conf
odt
xml
html
hta
py
ps
```

- https://github.com/lof1sec/Bad-ODF

- Fuerza bruta
```bash
hydra -l auctioneer -P /usr/share/wordlists/rockyou.txt gavel.htb http-post-form "/admin.php:user=^USER^&pass=^PASS^:Invalid password"
```
# NextJS exploit

https://github.com/alihussainzada/CVE-2025-29927-PoC/tree/main?tab=readme-ov-file

- Previous machine HTB

## LFI

- Rutas
```bash
/etc/apache2/sites-enabled/000-default.conf

/etc/squid/squid.conf


../../web.config
```

## DS_STORE

```bash
https://github.com/Keramas/DS_Walk
```

## IIS ShortScan

```bash
https://github.com/lijiejie/IIS_shortname_Scanner
```

