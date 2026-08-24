## Descripcion
To get truly 1337, you must understand different data encodings, such as hexadecimal or binary. Can you get the flag from this program to prove you are on the way to becoming 1337?
## Solucion

Vamos a usar 2 terminales, una para conectarnos al puerto y escribir las palabras decodificadas y otra para usar python y decodificar los cifrados
Primer bloque de codigo para la parabra encriptada en binario base 2
binarios = "01101100 01101001 01101101 01100101"
palabra = "".join([chr(int(b, 2)) for b in binarios.split()])
print(palabra)

Segundo bloque de codigo para la palarba encriptada en octal base 8

octales = "o160 o145 o141 o162"
palabra = "".join([chr(int(o.replace('o', ''), 8)) for o in octales.split()])
print(palabra)

Tercer bloque de texto para la palabra encriptada en hexadecimal base 16

hexadecimal = "636f6d7075746572"
palabra = bytes.fromhex(hexadecimal).decode("utf-8")
print(palabra)


## Notas adicionales

`binarios.split()`: Toma la cadena larga y la corta cada vez que encuentra un espacio. Nos devuelve una lista de fragmentos

`for b in ...`: Inicia un bucle donde la variable `b` será cada uno de esos fragmentos binarios.
`int(b, 2)`:  Convierte una cadena de texto a un número entero decimal

`"".join(...)`: El bucle nos devuelve una lista de letras sueltas `['l', 'i', 'm', 'e']`. Esta función las pega todas sin ningún separador (`""`) para formar la palabra final

- `o.replace('o', '')`: Antes de hacer matemáticas, tomamos el bloque (por ejemplo, `"o160"`) y le pedimos a Python que reemplace la letra "o" por nada (vacío). Esto "limpia" el dato y lo deja como `"160"`.
    
- `int(..., 8)`: Igual que antes, pero ahora le decimos a Python que el número que le entregamos está en Base 8 (octal). Él hace la conversión a decimal internamente

- `bytes.fromhex(hexadecimal)`: Toma la cadena de texto y la convierte directamente en un flujo de **bytes crudos (raw bytes)** en la memoria de la computadora. En este punto, no son letras, son señales eléctricas agrupadas.
    
- `.decode("utf-8")`: Toma esos bytes crudos y los "decodifica" usando el estándar UTF-8 (que incluye ASCII). Le dice a la computadora: _"Interpreta estos bytes como caracteres legibles por humanos"_

## Referencias