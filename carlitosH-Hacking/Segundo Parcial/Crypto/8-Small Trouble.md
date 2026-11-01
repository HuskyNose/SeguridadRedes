## Descripcion
Everything seems secure; strong numbers, familiar parameters but something small might ruin it all. Can you recover the message? Download the [message](https://challenge-files.cylabacademy.net/library/12a109dcb6df171263125b726d1065707a5a3907ca77783ca8d11693931443f0/message.txt). And source [code](https://challenge-files.cylabacademy.net/library/12a109dcb6df171263125b726d1065707a5a3907ca77783ca8d11693931443f0/encryption.py)
## Solucion

## 1. Idea y vulnerabilidad

El generador usa un exponente privado d de solo 256 bits, aunque n está formado por dos primos de 1048 bits cada uno. El exponente privado es demasiado pequeño para ese tamaño de módulo y permite el ataque de Wiener mediante fracciones continuas de e/n.

## 2. Procedimiento paso a paso

**1.** Lee n, e y c desde message.txt. El código original confirma que e es el inverso modular de d respecto de φ(n).

**2.** Calcula la expansión en fracciones continuas de e/n y genera sus convergentes k/d.

**3.** Para cada candidato calcula φ = (e × d − 1) / k, únicamente cuando la división es exacta.

**4.** Usa φ y n para obtener la suma de los factores: p + q = n − φ + 1. El discriminante (p + q)^2 − 4n debe ser un cuadrado perfecto.

**5.** Cuando se recuperan p y q y se verifica p × q = n, el candidato d es correcto. Descifra m = c^d mod n y convierte el entero a bytes.

## 3. Script de solución (solve.py)


```
from pathlib import Path

from math import isqrt

parametros = {}

for linea in Path("message.txt").read_text().splitlines():

    nombre, valor = linea.split(" = ", 1)

    parametros[nombre] = int(valor)

n = parametros["n"]

e = parametros["e"]

c = parametros["c"]

def fracciones_continuas(a, b):

    while b:

        q = a // b

        yield q

        a, b = b, a - q * b

def convergentes(secuencia):

    p_anterior, p_actual = 0, 1

    q_anterior, q_actual = 1, 0

    for termino in secuencia:

        p_nuevo = termino * p_actual + p_anterior

        q_nuevo = termino * q_actual + q_anterior

        yield p_nuevo, q_nuevo

        p_anterior, p_actual = p_actual, p_nuevo

        q_anterior, q_actual = q_actual, q_nuevo

clave_privada = None

for k, d in convergentes(fracciones_continuas(e, n)):

    if k == 0 or (e * d - 1) % k != 0:

        continue

    phi = (e * d - 1) // k

    suma = n - phi + 1

    discriminante = suma * suma - 4 * n

    if discriminante < 0:

        continue

    raiz = isqrt(discriminante)

    if raiz * raiz != discriminante or (suma + raiz) % 2 != 0:

        continue

    p = (suma + raiz) // 2

    q = (suma - raiz) // 2

    if p * q == n:

        clave_privada = d

        break

if clave_privada is None:

    raise ValueError("No se encontró d; el ataque de Wiener no recuperó la clave")

m = pow(c, clave_privada, n)

texto = m.to_bytes((m.bit_length() + 7) // 8, "big")

print("d recuperado:", clave_privada)

print("Bandera:", texto.decode("utf-8"))
```

## Notas adicionales

## Referencias