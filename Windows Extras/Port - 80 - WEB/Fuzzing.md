
- Sacar subdominios
```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt -u 'http://planning.htb/' -H 'Host: FUZZ.planning.htb' -fs 178
```

- Directorio
```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u 'http://environment.htb/FUZZ'

```

- Usuarios
```bash
ffuf -u 'http://nocturnal.htb/view.php?username=FUZZ&file=*.pdf' -w
/usr/share/seclists/Usernames/xato-net-10-million-usernames.txt -mc 200 -fr
"User not found." -H "Cookie: PHPSESSID=4d9uqe8ifkefg1pkgu5ksi06qs
```
