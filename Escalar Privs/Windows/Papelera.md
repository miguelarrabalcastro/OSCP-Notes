- Ver si hay algo
```powershell
$shell = New-Object -ComObject Shell.Application
$recycleBin = $shell.Namespace(0xA)
$recycleBin.items() | Select-Object Name, Path
```

- Sacarlo
```powershell
$recycleBin = (New-Object -ComObject Shell.Application).NameSpace(0xA)  
$items = $recycleBin.Items()  
$item = $items | Where-Object {$_.Name -eq "wapt-backup-sunday.7z"}  
$documentsPath = [Environment]::GetFolderPath("Desktop")  
$documents = (New-Object -ComObject Shell.Application).NameSpace($documentsPath)  
$documents.MoveHere($item)
```


## Ver usuarios borrados

```powershell
get-adobject -Filter {Deleted -eq $true -and ObjectClass -eq "user"} -IncludeDeletedObjects

get-adobject -Filter {Deleted -eq $true -and ObjectClass -eq "user"} -IncludeDeletedObjects -Properties *
```
