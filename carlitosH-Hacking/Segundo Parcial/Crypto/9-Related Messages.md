## Descripcion
Oops! I have a typo in my first message so i sent it again! I used RSA twice so this is secure right? [chall.py](https://challenge-files.cylabacademy.net/library/d33371f1a01fd9671ac08d9ce0a486325fd0e8ed66ce83fc97ee9a5a07a64cb9/chall.py) [output.txt](https://challenge-files.cylabacademy.net/library/d33371f1a01fd9671ac08d9ce0a486325fd0e8ed66ce83fc97ee9a5a07a64cb9/output.txt)
## Solucion

## 1. Idea y vulnerabilidad

Se cifra dos veces con el mismo módulo RSA y exponente e = 17. Los mensajes son casi iguales: el archivo indica Message − Message_fixed = −3, así que el segundo mensaje es el primero más 3. La relación conocida permite aplicar el ataque Franklin-Reiter.

## 2. Procedimiento paso a paso

**1.** Lee c1, c2, la diferencia y N desde output.txt. El exponente público está en chall.py: e = 17.

**2.** Define M como el primer mensaje. Debido a que M − M_fixed = −3, el segundo mensaje es M + 3.

**3.** Construye los polinomios F1(x) = x^17 − c1 y F2(x) = (x + 3)^17 − c2, trabajando módulo N.

**4.** Calcula el máximo común divisor polinómico de F1 y F2 mediante el algoritmo de Euclides. El resultado monico es lineal: x − M.

**5.** Obtén M a partir del término independiente y suma 3 para recuperar el segundo mensaje. Verifica ambos cifrados elevándolos a la potencia 17 módulo N.


## 3. Script de solución (solve.py)


```
from pathlib import Path

from math import comb, gcd

lineas = Path("output.txt").read_text().splitlines()

c1 = int(lineas[0])

c2 = int(lineas[1])

diferencia = int(lineas[2])  # Message - Message_fixed = -3

n = int(lineas[3])

e = 17

# Polinomios representados con coeficientes de menor a mayor grado.

def recortar(a):

    while len(a) > 1 and a[-1] % n == 0:

        a.pop()

    return a

def restar(a, b):

    resultado = [0] * max(len(a), len(b))

    for i in range(len(resultado)):

        x = a[i] if i < len(a) else 0

        y = b[i] if i < len(b) else 0

        resultado[i] = (x - y) % n

    return recortar(resultado)

def multiplicar_escalar(a, k):

    return recortar([(x * k) % n for x in a])

def desplazar(a, cantidad):

    return [0] * cantidad + a

def residuo(a, b):

    a = a[:]

    while len(a) >= len(b) and not (len(a) == 1 and a[0] == 0):

        desplazamiento = len(a) - len(b)

        try:

            inverso_lider = pow(b[-1], -1, n)

        except ValueError:

            factor = gcd(b[-1], n)

            raise ValueError(f"Coeficiente no invertible; gcd con N = {factor}")

        factor = (a[-1] * inverso_lider) % n

        a = restar(a, multiplicar_escalar(desplazar(b, desplazamiento), factor))

    return recortar(a)

# M es el primer mensaje. Como M - M_fixed = -3, el segundo es M + 3.

# F1(x) = x^e - c1; F2(x) = (x + 3)^e - c2.

F1 = [(-c1) % n] + [0] * (e - 1) + [1]

F2 = [(comb(e, i) * pow(3, e - i, n)) % n for i in range(e + 1)]

F2[0] = (F2[0] - c2) % n

# Algoritmo de Euclides polinómico módulo N: Franklin-Reiter.

a, b = F1, F2

while not (b == [0]):

    a, b = b, residuo(a, b)

inverso_lider = pow(a[-1], -1, n)

gcd_monomico = multiplicar_escalar(a, inverso_lider)

if len(gcd_monomico) != 2:

    raise ValueError("El máximo común divisor no resultó lineal")

mensaje1 = (-gcd_monomico[0]) % n

mensaje2 = (mensaje1 + 3) % n

def a_bytes(numero):

    return numero.to_bytes((numero.bit_length() + 7) // 8, "big")

texto1 = a_bytes(mensaje1).decode("utf-8")

texto2 = a_bytes(mensaje2).decode("utf-8")

print("Primer mensaje (con el error):", texto1)

print("Segundo mensaje (corregido):", texto2)

print("Verificación:", pow(mensaje1, e, n) == c1 and pow(mensaje2, e, n) == c2)
```

## Notas adicionales

## Referencias
