## Descripcion
How to automate tasks to run at intervals on linux servers?

Use ssh to connect to this server:

`Server: saturn.picoctf.net Port: 56987 Username: picoplayer Password: H9RmN0m18U`
## Solucion
ejecutamos:
```
ssh -p 56987 picoplayer@saturn.picoctf.net
```
Para entrar
Ejecutamos los siguientes comandos 
picoplayer@challenge:~$ crontab -l
no crontab for picoplayer
picoplayer@challenge:~$ cat /etc/crontab
# picoCTF{Sch3DUL7NG_T45K3_L1NUX_d83baed1}
## Notas adicionales
usuario en Linux puede tener su propia lista de tareas programadas. Revisa si tu usuario actual tiene alguna configurada ejecutando: `crontab -l`
## Referencias
