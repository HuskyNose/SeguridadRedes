## Descripcion
A new modular challenge! Download the message [here](https://challenge-files.cylabacademy.net/library/8493f8b1c07d84e858fa52d3dacdc63752275286da7a30b69fab36993eafb5ea/message.txt).

Take each number mod 41 and find the modular inverse for the result. Then map to the following character set: 1-26 are the alphabet, 27-36 are the decimal digits, and 37 is an underscore.

Wrap your decrypted message in the academy flag format (i.e. `academy{decrypted_message}`)
## Solucion
## 1. Idea y vulnerabilidad

El reto transforma cada número tomando su residuo módulo 41 y después aplica el inverso multiplicativo. El inverso es el número x que cumple (residuo × x) mod 41 = 1. Como 41 es primo y los residuos no son cero, todos tienen inverso.

## 2. Procedimiento paso a paso

**1.** Abre message.txt y separa los 23 números que contiene.

**2.** Para cada número calcula el residuo módulo 41: por ejemplo, 432 mod 41 = 22.

**3.** Calcula el inverso multiplicativo del residuo. Para el ejemplo, el inverso de 22 módulo 41 es 28, porque 22 × 28 mod 41 = 1.

**4.** Convierte cada inverso al alfabeto indicado: 1–26 → a–z; 27–36 → 0–9; 37 → guion bajo. Por ejemplo, 28 representa el dígito 1.

**5.** Une los caracteres en el mismo orden .


## 3. Script de solución (solve.py)


```

from pathlib import Path

numeros = list(map(int, Path("message.txt").read_text().split()))

alfabeto = "abcdefghijklmnopqrstuvwxyz"

resultado = ""

for numero in numeros:

    residuo = numero % 41

    inverso = pow(residuo, -1, 41)

    if 1 <= inverso <= 26:

        resultado += alfabeto[inverso - 1]

    elif 27 <= inverso <= 36:

        resultado += str(inverso - 27)

    elif inverso == 37:

        resultado += "_"

    else:

        raise ValueError(f"Valor fuera del alfabeto: {inverso}")

print("Mensaje:", resultado)

print("Bandera: academy{" + resultado + "}")
```
## Notas adicionales

## Referencias
