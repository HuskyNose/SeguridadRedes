## Descripcion
Why use p and q when I can use more? Connect with `nc xebec.cylabacademy.net 37843`.
## Solucion
```
  

from sympy import factorint

from math import prod

  

c = int(input("Introduce c: "))

n = int(input("Introduce n: "))

e = int(input("Introduce e: "))

  

print("\nFactorizando N...")

factores = factorint(n)

  

print("Factores encontrados:")

print(factores)

  

# Calcular phi(N), considerando las multiplicidades

phi = prod(

    p ** (exp - 1) * (p - 1)

    for p, exp in factores.items()

)

  

# Calcular la clave privada

d = pow(e, -1, phi)

  

# Descifrar

m = pow(c, d, n)

  

mensaje = m.to_bytes((m.bit_length() + 7) // 8, "big")

  

print("\nMensaje en bytes:")

print(mensaje)

  

print("\nTexto descifrado:")

print(mensaje.decode("utf-8", errors="replace"))
```
## Notas adicionales
Puede tardar varios minutos en cargar la factorizacion
## Referencias
