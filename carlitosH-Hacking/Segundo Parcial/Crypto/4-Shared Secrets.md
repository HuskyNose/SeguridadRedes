## Descripcion
A message was encrypted using a shared secret... but it looks like one side of the exchange leaked something. Can you piece together the secret and get the flag? Download the [message](https://challenge-files.cylabacademy.net/library/0c5716023de07c8f5e39852dad85c3c416bb8de0fb7fb3216ae79dd5bf1a58e3/message.txt). And source [code](https://challenge-files.cylabacademy.net/library/0c5716023de07c8f5e39852dad85c3c416bb8de0fb7fb3216ae79dd5bf1a58e3/encryption.py)
## Solucion

## 1. Idea y vulnerabilidad

El código usa Diffie-Hellman para crear un secreto compartido y luego cifra la bandera con XOR. El archivo message.txt expone el secreto privado b del cliente, por lo que el secreto compartido se puede calcular sin resolver el logaritmo discreto.

## 2. Procedimiento paso a paso

**1.** Lee los parámetros g, p, A y b junto con el texto cifrado en hexadecimal.

**2.** Recuerda que A = g^a mod p. El secreto compartido puede calcularse como A^b mod p, porque b fue filtrado.

**3.** Calcula shared = pow(A, b, p). En este reto, shared mod 256 es 107.

**4.** El cifrado aplica el mismo byte shared mod 256 a cada byte mediante XOR. Repite la operación para recuperar el texto: byte_claro = byte_cifrado XOR 107.

**5.** Decodifica los bytes recuperados como UTF-8.


## 3. Script de solución (solve.py)

```
from pathlib import Path

parametros = {}

for linea in Path("message.txt").read_text().splitlines():

    nombre, valor = linea.split(" = ", 1)

    if nombre == "enc":

        parametros[nombre] = bytes.fromhex(valor)

    else:

        parametros[nombre] = int(valor)

g = parametros["g"]

p = parametros["p"]

A = parametros["A"]

b = parametros["b"]  # El secreto del cliente fue filtrado.

cifrado = parametros["enc"]

# DH: el secreto compartido es A^b mod p.

secreto_compartido = pow(A, b, p)

byte_clave = secreto_compartido % 256

# La función de cifrado XOR-eó cada byte con el mismo byte de clave.

texto = bytes(byte ^ byte_clave for byte in cifrado)

print("Secreto compartido (mod 256):", byte_clave)

print("Bandera:", texto.decode("utf-8"))
```


## Notas adicionales

## Referencias
