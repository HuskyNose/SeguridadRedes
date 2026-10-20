## Descripcion
In RSA, a small ee value can be problematic, but what about NN? Can you decrypt this? [values](https://challenge-files.cylabacademy.net/library/4a3b1aca528881eece43ed483e527d3700c5e388eb5ab2291015dbd67a809f31/values)
## Solucion
```

# Valores del archivo values
c = int(input("Introduce c: "))
N = int(input("Introduce N: "))
e = int(input("Introduce e: "))

# Factores encontrados en FactorDB
p = int(input("Introduce p: "))
q = int(input("Introduce q: "))

# Calcular la funcion phi de N
phi = (p - 1) * (q - 1)

# Calcular la clave privada
d = pow(e, -1, phi)

# Descifrar el mensaje
m = pow(c, d, N)

# Convertir el entero a texto
mensaje = m.to_bytes((m.bit_length() + 7) // 8, "big")

print("\nClave privada d:", d)
print("Mensaje en bytes:", mensaje)
print("Mensaje descifrado:")

try:
    print(mensaje.decode("utf-8"))
except UnicodeDecodeError:
    print(mensaje.decode("utf-8", errors="replace"))

```
## Notas adicionales
https://factordb.com/?id=1100000010656148435
Se uso para factorizar n
## Referencias
