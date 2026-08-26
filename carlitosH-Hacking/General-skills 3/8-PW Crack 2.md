## Descripcion
Can you crack the password to get the flag?

Download the password checker [here](https://artifacts.picoctf.net/c/15/level2.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/15/level2.flag.txt.enc) in the same directory too.
## Solucion
Lo mismo que el anterior, solo que esta vez al abrir el editor la contraseña estara encriptada con ascii, copiamos los caracteres a desincriptar y solo lo pasamos por python
```
chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65)
```
Nos dara la contraseña, la colocamos en el script level 2 y listo ahi estara la bandera
```
C:\Users\Husky\Desktop\Trabajos\redes>python level2.py
Please enter correct password for flag: 39ce
Welcome back... your flag, user:
picoCTF{tr45h_51ng1ng_502ec42e
```
## Notas adicionales

## Referencia