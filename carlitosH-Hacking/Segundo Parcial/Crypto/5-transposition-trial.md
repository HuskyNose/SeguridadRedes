## Descripcion
Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message. Download the corrupted message [here](https://challenge-files.cylabacademy.net/library/c432352dd1b936c7ab4ceb162b63dafa1292c57462d832c59614d4db0de130be/message.txt).
## Solucion
## 1. Idea y vulnerabilidad

El reto indica que los caracteres se reordenaron en grupos de tres, sin reemplazarlos. La primera palabra parece tener tres letras. Al probar las seis permutaciones posibles, el orden [2, 0, 1] reconstruye “The flag is ...”.

## 2. Procedimiento paso a paso

**1.** Divide el texto cifrado en bloques consecutivos de tres caracteres.

**2.** Prueba las seis permutaciones posibles de las posiciones 0, 1 y 2 en un bloque. Para el primer bloque heT, el orden [2, 0, 1] produce The.

**3.** Aplica esa misma permutación a todos los bloques: toma el tercer carácter, luego el primero y finalmente el segundo.


## 3. Script de solución (solve.py)

```
from pathlib import Path

cifrado = Path("message.txt").read_text().strip()

if len(cifrado) % 3 != 0:

    raise ValueError("La longitud del mensaje no es múltiplo de 3")

resultado = ""

for i in range(0, len(cifrado), 3):

    bloque = cifrado[i:i + 3]


    resultado += bloque[2] + bloque[0] + bloque[1]

print("Mensaje:", resultado)

print("Bandera:", resultado[resultado.find("academy{"):resultado.find("}", resultado.find("academy{")) + 1])
```

## Notas adicionales

## Referencias
