## Descripcion
Can you get sense of this code file and write the function that will decode the given encrypted file content.

Find the encrypted file here [flag_info](https://challenge-files.cylabacademy.net/library/c5a30495112ed010f3131d9c91bc11efa2c005dfda1262f5c64d434f43a3bbc2/enc_flag) and [code file](https://challenge-files.cylabacademy.net/library/c5a30495112ed010f3131d9c91bc11efa2c005dfda1262f5c64d434f43a3bbc2/custom_encryption.py) might be good to analyze and get the flag.
## Solucion
## 1. Idea y vulnerabilidad

La rutina combina dos capas reversibles. Primero aplica XOR a la cadena invertida usando la clave repetida “trudeau”. Después multiplica cada código de carácter por shared × 311. Los valores a y b filtrados permiten reconstruir shared mediante Diffie-Hellman.

## 2. Procedimiento paso a paso

**1.** Lee a = 95, b = 31 y la lista cipher desde enc_flag.

**2.** Usa p = 97 y g = 31, tal como aparecen en custom_encryption.py. Calcula u = g^a mod p = 72 y v = g^b mod p = 95.

**3.** Calcula shared = v^a mod p = 48. El segundo acuerdo de claves produce el mismo valor.

**4.** La primera capa de cifrado multiplicó cada código ASCII por shared × 311 = 14928. Divide cada elemento de cipher entre 14928 y convierte el cociente a carácter.

**5.** El resultado es el texto tras el XOR, pero todavía está invertido. Aplica XOR con la clave repetida “trudeau” y luego invierte la cadena para recuperar la bandera.


## 3. Script de solución (solve.py)


```
from pathlib import Path

import ast

contenido = Path("enc_flag").read_text()

a = int(next(line.split("=", 1)[1] for line in contenido.splitlines() if line.startswith("a =")))

b = int(next(line.split("=", 1)[1] for line in contenido.splitlines() if line.startswith("b =")))

linea_cifrado = next(line for line in contenido.splitlines() if line.startswith("cipher is:"))

cifrado = ast.literal_eval(linea_cifrado.split(":", 1)[1].strip())

p = 97

g = 31

u = pow(g, a, p)

v = pow(g, b, p)

secreto_compartido = pow(v, a, p)


semicifrado = "".join(chr(valor // (secreto_compartido * 311)) for valor in cifrado)

clave_textual = "trudeau"

texto_invertido = "".join(

    chr(ord(caracter) ^ ord(clave_textual[i % len(clave_textual)]))

    for i, caracter in enumerate(semicifrado)

)

texto = texto_invertido[::-1]

print("u =", u, "v =", v)

print("Secreto compartido =", secreto_compartido)

print("Bandera:", texto)
```

## Notas adicionales

## Referencias
