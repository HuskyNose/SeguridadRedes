## Descripcion
In RSA d is a lot bigger than e, why don't we use d to encrypt instead of e?
## Solucion
```
  

c = int(input("Introduce c: "))

n = int(input("Introduce n: "))

  

m = pow(c, 65537, n)

  

mensaje = m.to_bytes((m.bit_length() + 7) // 8, "big")

  

print("Mensaje en bytes:", mensaje)

print("Texto:")

print(mensaje.decode("utf-8", errors="replace"))
```
## Notas adicionales

## Referencias