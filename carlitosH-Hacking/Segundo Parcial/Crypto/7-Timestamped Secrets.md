## Descripcion
Someone encrypted a message using AES in ECB mode but they weren’t very careful with their key. Turns out it’s derived from something as simple as the current time! Can you uncover the key and decrypt the flag? Download the encrypted message: [message](https://challenge-files.cylabacademy.net/library/838909e4e064bca5edc41edd46ebb4f8350eb82f2aea2540ea564e491c6d437e/message.txt)  
You may also find the encryption script helpful: [code](https://challenge-files.cylabacademy.net/library/838909e4e064bca5edc41edd46ebb4f8350eb82f2aea2540ea564e491c6d437e/encryption.py)
## Solucion
## 1. Idea y vulnerabilidad

AES-ECB se usa con una clave derivada de una marca de tiempo. El archivo proporciona la hora aproximada y el script indica la derivación: SHA-256 del timestamp convertido a texto, tomando los primeros 16 bytes como clave AES-128.

## 2. Procedimiento paso a paso

**1.** Lee la marca de tiempo indicada en message.txt: 1790147519 UTC (23 de septiembre de 2026, 07:11:59 UTC).

**2.** Convierte el timestamp a su representación decimal en texto y calcula SHA-256 de esos bytes.

**3.** Toma los primeros 16 bytes del resumen como clave AES-128.

**4.** Convierte el ciphertext hexadecimal a bytes y descífralo usando AES en modo ECB.

**5.** Retira el relleno PKCS#7 de bloque de 16 bytes y decodifica el texto como UTF-8.

## 3. Script de solución (solve.py)


```
from pathlib import Path

import hashlib

from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes

from cryptography.hazmat.primitives.padding import PKCS7

contenido = Path("message.txt").read_text()

timestamp = int(contenido.split("Hint: The encryption was done around ", 1)[1].split()[0])

hex_cifrado = contenido.split("Ciphertext (hex): ", 1)[1].strip()

cifrado = bytes.fromhex(hex_cifrado)

clave = hashlib.sha256(str(timestamp).encode()).digest()[:16]

descifrador = Cipher(algorithms.AES(clave), modes.ECB()).decryptor()

texto_con_relleno = descifrador.update(cifrado) + descifrador.finalize()

desempaquetador = PKCS7(128).unpadder()

texto = desempaquetador.update(texto_con_relleno) + desempaquetador.finalize()

print("Timestamp usado:", timestamp)

print("Bandera:", texto.decode("utf-8"))
```

## Notas adicionales

## Referencias
