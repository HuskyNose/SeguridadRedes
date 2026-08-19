## Descripcion
Our flag printing service has started glitching!

`$ nc saturn.picoctf.net 60620`


ASCII is one of the most common encodings used in programming

We know that the glitch output is valid Python, somehow!

Press Ctrl and c on your keyboard to close your connection and return to the command prompt.
## Solucion
```
HuskyNose-academy@webshell:~$ python
Python 3.10.12 (main, Mar  3 2026, 11:56:32) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 'picoCTF{gl17ch_m3_n07_' + chr(0x39) + chr(0x63) + chr(0x34) + chr(0x32) + chr(0x61) + chr(0x34) + chr(0x35) + chr(0x64) + '}'
'picoCTF{gl17ch_m3_n07_9c42a45d}'
```

## Notas adicionales
Python utiliza el 6 para concetar cadenas
chr{}es una función de python  que convierte un numero a su correspondiente carácter ASCII
solo fue una suma de caracteres
## Referencias
