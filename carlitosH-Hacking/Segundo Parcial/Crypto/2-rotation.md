## Descripcion
You will find the flag after decrypting this file Download the encrypted flag [here](https://challenge-files.cylabacademy.net/library/ee237b7e28b6b3871ce9d37f01093b13c190138d2be22fcae22865975e362c1f/encrypted.txt).
## Solucion
## 1. Idea y vulnerabilidad

El texto está cifrado mediante una rotación de letras. Los números, las llaves y los guiones bajos se conservan. Al probar los desplazamientos se identifica ROT8: para descifrar, cada letra se mueve ocho posiciones hacia atrás en el alfabeto.

## 2. Procedimiento paso a paso

**1.** Abre encrypted.txt. El texto empieza con ikilmug.

**2.** Prueba desplazamientos sobre las letras minúsculas. Con un desplazamiento de 8 hacia atrás, ikilmug se convierte en academy.

**3.** Aplica la misma operación a todas las letras. Conserva números y signos sin modificarlos.

**4.** El texto resultante ya contiene la bandera completa; no es necesario volver a envolverla.



## 3. Script de solución (solve.py)

```
from pathlib import Path

cifrado = Path("encrypted.txt").read_text().strip()

desplazamiento = 8

resultado = ""

for caracter in cifrado:

    if "a" <= caracter <= "z":

        nuevo = (ord(caracter) - ord("a") - desplazamiento) % 26

        resultado += chr(nuevo + ord("a"))

    else:

        resultado += caracter

print("Mensaje:", resultado)

print("Bandera:", resultado)
```
## Notas adicionales

## Referencias
