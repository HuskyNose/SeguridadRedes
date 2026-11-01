## Descripcion
You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag. Download the jpg image [here](https://challenge-files.cylabacademy.net/library/714093cf55b6f82d117c53a2a1d44f4956e0ccc7655b1fe2efee99e12b314f53/img.jpg).
## Solucion

```
from PIL import Image

import base64

  

comentario = Image.open("img.jpg").info["comment"].decode("ascii")

pista = base64.b64decode(comentario).decode("ascii")

herramienta, clave_b64 = pista.split(":", 1)

clave = base64.b64decode(clave_b64).decode("ascii")

print("Herramienta:", herramienta)

print("Contraseña:", clave)

print("Ahora ejecuta: steghide extract -sf img.jpg -p", clave)
```
## Notas adicionales

## Referencias
https://sourceforge.net/projects/steghide/