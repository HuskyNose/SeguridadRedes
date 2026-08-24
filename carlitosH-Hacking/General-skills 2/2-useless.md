## Descripcion

There's an interesting script in the user's home directory

The work computer is running SSH. We've been given a script which performs some basic calculations, explore the script and find a flag.

`Hostname: saturn.picoctf.net Port: 56473 Username: picoplayer Password: password`

## Solucion

nos conectamos a la maquina prestada 
ssh picoplayer@saturn.picoctf.net -p 60536

colocamos la contraseña que nos dio
usamos el comando ls -la para ver todos los archivos y los ocultos
```

total 16
drwxr-xr-x 1 picoplayer picoplayer   20 Aug 24 02:53 .
drwxr-xr-x 1 root       root         24 Aug  4  2023 ..
-rw-r--r-- 1 picoplayer picoplayer  220 Feb 25  2020 .bash_logout
-rw-r--r-- 1 picoplayer picoplayer 3771 Feb 25  2020 .bashrc
drwx------ 2 picoplayer picoplayer   34 Aug 24 02:53 .cache
-rw-r--r-- 1 picoplayer picoplayer  807 Feb 25  2020 .profile
-rwxr-xr-x 1 root       root        517 Mar 16  2023 useless

```

aqui podemos ver que el script que necesitamos acceder es el de useless, cuando vemos una herramienta no conocida, usamos `man`, `man useless`
## Notas adicionales
En Linux, la herramienta `man` (de _manual_) es tu biblioteca integrada. Sirve para leer la documentación oficial de los comandos, programas y scripts instalados en el sistema

Cuando encontramos una herramienta desconocida en un servidor, antes de ejecutarla a ciegas (lo cual podría ser peligroso), leemos su manual para entender qué hace, qué parámetros acepta y quién la creó
## Referencias