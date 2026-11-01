## Descripcion
Download this image file and find the flag.

- [Download image file](https://challenge-files.cylabacademy.net/library/248587d9a868db74a285623697f78ef3d87561aaa16ff1fb211fe88cd72f4a6c/drawing.flag.svg)
## Solucion

Aunque parece una imagen vectorial, SVG es XML y contiene texto legible en su estructura. La cadena está dibujada con texto blanco diminuto sobre fondo blanco, por lo que casi no se distingue al abrirla como imagen.

```
import xml.etree.ElementTree as ET  
import re  
  
raiz = ET.parse("drawing.flag.svg").getroot()  
texto = "".join(raiz.itertext())  
texto = re.sub(r"\s+", "", texto)  
  
m = re.search(r"academy\{[^}]+\}", texto)  
print(m.group(0) if m else "No se encontró la bandera")
```

## Notas adicionales

## Referencias
