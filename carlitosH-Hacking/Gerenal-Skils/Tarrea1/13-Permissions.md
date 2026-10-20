## Descripcion
Can you read files in the root file?

The system admin has provisioned an account for you on the main server:

`ssh -p 58101 [picoplayer@saturn.picoctf.net](mailto:picoplayer@saturn.picoctf.net)`

Password: `33qE7mB5BF`

Can you login and read the root file?
## Solucion
Una vez conectados usamos sudo -l para ver que programas podemos ejecutar. Vemos que tenemos habilitado el editor de texto "vi" por lo que usamos sudo vi para abrirlo, presionamos esc varias veces, despues ponemos ":"  y ejecutamos:
```
:!/bin/bash
```
despes la terminal colapsara, solo escribimos whoami, ya solo queda lanzar un:
```
ls -la /root
```
Para ver los archivos y el nombre de la bandera, ya solo ejecutamos:
```
cat root/.flag.txt
```
Y la bandera sera nuestra 
picoCTF{uS1ng_v1m_3dit0r_3dd6dcf4}

## Notas adicionales

## Referencias
