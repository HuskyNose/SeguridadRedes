## Descripcion
This service can provide you with a random number, but can it do anything else? Connect to the program with netcat:

$ nc chatelaine.cylabacademy.net 23068

The program's source code can be downloaded here

.
## Solucion
dentro del .py esta esta parte del codifo:
```
def win():
    flag = open('flag.txt', 'r').read()
    flag = flag.strip()
    str_flag = ''

    for c in flag:
        str_flag += str(hex(ord(c))) + ' '

    print(str_flag)
```

No imprime la bandera sin no que la imprime en caracteres hexadecimales, por lo que colocando win en la terminal nos dara los valores, ya solo queda convertir los valores 
## Notas adicionales

## Referencias
