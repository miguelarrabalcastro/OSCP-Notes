
- Ver que tiene
```bash
showmount -e 10.10.11.78
```

- Si hay algo lo levantamos en local
```bash
mkdir /tmp/mirage

sudo mount -t nfs 10.10.11.78:/MirageReports /tmp/mirage

cd /tmp/mirage

ls
```
