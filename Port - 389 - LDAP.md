
```bash
ldapsearch -x -H ldap://$IP -s base namingcontexts

ldapsearch -x -H ldap://10.10.10.182 -b "DC=cascade,DC=local"

ldapsearch -x -H ldap://10.10.11.174 -D 'ldap@support.htb' -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "DC=support,DC=HTB"

ldapsearch -H ldap://192.168.123.122 -x -b "dc=hutch,dc=offsec" "(objectClass=person)" | grep -E "sAMAccountName|description"
```
- Filtramos por `CN` para sacar usuarios y montar un diccionarios de posibles combinaciones
```java
h.smith
hugo.smith
hugosmith
hsmith
```

## Enumeracion

-  https://github.com/ropnop/windapsearch
- pip install python-ldap

```bash
./windapsearch.py -U --full --dc-ip 10.10.10.182
```
