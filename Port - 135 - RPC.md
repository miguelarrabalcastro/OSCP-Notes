```bash
rpcclient -U "" 10.10.10.175 -N

rpcclient $> enumdomusers
```

- Si tengo credenciales
```bash
rpcclient -U "fsmith%Thestrokes23" 10.10.10.175
```

- Comandos
```bash
rpcclient $> enumdomusers

rpcclient $> enumdomgroups

rpcclient $> querygroupmem $RID
rpcclient $> queryuser $RID
rpcclient $> s
```

- Sacar usuario
```bash
rpcclient -U "judith.mader%judith09" 10.10.11.41 -c enumdomusers | grep -oP '\[.*?\]' | grep -v '0x'| tr -d '[]' 
```
