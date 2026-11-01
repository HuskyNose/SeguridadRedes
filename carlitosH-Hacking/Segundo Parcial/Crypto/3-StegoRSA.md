## Descripcion
A message has been encrypted using RSA. The public key is gone… but someone might have been careless with the private key. Can you recover it and decrypt the message? Download the [flag](https://challenge-files.cylabacademy.net/library/cd170c0e341c181c93172139e85c2b00cb4d64184768c43706a6ac8234903dbe/flag.enc) and [image](https://challenge-files.cylabacademy.net/library/cd170c0e341c181c93172139e85c2b00cb4d64184768c43706a6ac8234903dbe/image.jpg).
## Solucion
## 1. Idea y vulnerabilidad

La clave pública no está disponible, pero la imagen JPEG contiene un comentario (COM) con el texto hexadecimal de una clave privada RSA en formato PEM. La debilidad no está en RSA: la clave privada se filtró dentro de los metadatos de la imagen.

## 2. Procedimiento paso a paso

**1.** Inspecciona los metadatos de image.jpg. El comentario JPEG contiene una cadena hexadecimal que empieza con el texto codificado de -----BEGIN PRIVATE KEY-----.

**2.** Convierte ese hexadecimal a bytes. El resultado es el PEM de la clave privada RSA.

**3.** Importa la clave con load_pem_private_key y lee flag.enc como bytes binarios.

**4.** Descifra el bloque RSA con el esquema PKCS#1 v1.5. El archivo cifrado tiene 256 bytes, coherente con una clave RSA de 2048 bits.

**5.** Decodifica los bytes resultantes como UTF-8 

## 3. Script de solución (solve.py)

```
from pathlib import Path

from PIL import Image

from cryptography.hazmat.primitives.serialization import load_pem_private_key

from cryptography.hazmat.primitives.asymmetric import padding

comentario_hex = Image.open("image.jpg").info["comment"].decode("ascii")

clave_pem = bytes.fromhex(comentario_hex)

clave_privada = load_pem_private_key(clave_pem, password=None)

cifrado = Path("flag.enc").read_bytes()

texto = clave_privada.decrypt(cifrado, padding.PKCS1v15())

print("Bandera:", texto.decode("utf-8").strip())
```

## Notas adicionales

## Referencias
