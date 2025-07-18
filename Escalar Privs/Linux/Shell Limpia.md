
```bash
script /dev/null -c bash

Control+Z
stty raw -echo; fg
	reset xterm

export TERM=xterm
stty rows 39 columns 157
```
