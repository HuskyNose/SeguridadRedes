## Descripcion
This file doesn't look like much... just a bunch of 1s and 0s. But maybe it's not just random noise. Can you recover anything meaningful from this? Download the file [here](https://challenge-files.cylabacademy.net/library/4f119c7324ffc27875b984a1d0db0591c4214fa81bd566946f1d08ed29f35135/digits.bin).
## Solucion
```
from pathlib import Path  
from PIL import Image  
  
bits = Path("digits.bin").read_text(encoding="ascii").strip()  
if set(bits) - {"0", "1"}:  
    raise ValueError("El archivo contiene caracteres distintos de 0 y 1")  
if len(bits) % 8 != 0:  
    raise ValueError("La cantidad de bits no es múltiplo de 8")  
  
contenido = bytes(int(bits[i:i+8], 2) for i in range(0, len(bits), 8))  
Path("recovered.jpg").write_bytes(contenido)  
im = Image.open("recovered.jpg")  
print("JPEG recuperado:", im.size)  
im.show()
```
## Notas adicionales

## Referencias
