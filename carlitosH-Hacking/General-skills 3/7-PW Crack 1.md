## Descripcion
Can you crack the password to get the flag?

Download the password checker [here](https://artifacts.picoctf.net/c/10/level1.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/10/level1.flag.txt.enc) in the same directory too.
## Solucion
Abrimos el script con nano nuevamente y solo buscamos el bloque donde la contraseña compara el input del usuario, ahi esta la contraseña, solo copiamos la contraseña, ejecutamos el script y colocamos la contraseña y ahi estara la bandera

```
C:\Users\Husky\Desktop\Trabajos\redes>python level1.py
Please enter correct password for flag: 691d
Welcome back... your flag, user:
picoCTF{545h_r1ng1ng_56891419}
```
## Notas adicionales

## Referencias
