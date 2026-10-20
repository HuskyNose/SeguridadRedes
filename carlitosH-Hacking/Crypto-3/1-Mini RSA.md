## Descripcion
What happens if you have a small exponent? There is a twist though, we padded the plaintext so that (M∗∗e)(M∗∗e) is just barely larger than NN. Let's decrypt this: [values](https://challenge-files.cylabacademy.net/library/e5f3ed71ca30832720bfbed988000b07159531af4efd8bde534455cb31281df7/values)
## Solucion
```
  

import re

  

# Leer los valores del reto

archivo = open("values.txt", "r")

datos = archivo.read()

archivo.close()

  

N = int(re.search(r"N:\s*(\d+)", datos).group(1))

e = int(re.search(r"e:\s*(\d+)", datos).group(1))

c = int(re.search(r"ciphertext\s*\(c\):\s*(\d+)", datos).group(1))

  

print("Exponente:", e)

print("Iniciando busqueda...")

  

# Calcular la raiz cubica entera sin perder precision

def raiz_cubica(n):

    x = 1 << ((n.bit_length() + 2) // 3)

  

    while True:

        y = (2 * x + n // (x * x)) // 3

  

        if y >= x:

            return x

  

        x = y

  

# Buscar k hasta obtener una potencia exacta

k = 0

  

while True:

    valor = c + k * N

    m = raiz_cubica(valor)

  

    if m ** e == valor:

        mensaje = m.to_bytes((m.bit_length() + 7) // 8, "big")

  

        print("Encontrado k =", k)

        print("Mensaje en bytes:", mensaje)

        print("Mensaje decodificado:")

  

        try:

            print(mensaje.decode("utf-8"))

        except UnicodeDecodeError:

            print(mensaje.decode("utf-8", errors="replace"))

  

        break

  

    k = k + 1

  

    if k % 10000 == 0:

        print("Probando k =", k)
```
## Notas adicionales

## Referencias
