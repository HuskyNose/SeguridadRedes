## Descripcion
Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered. Find the PDF file here [Hidden Confidential Document](https://challenge-files.cylabacademy.net/library/b32f1f1945481591df61d328d02995fe3521d16b70928fbe44e3bd90c4ccb113/confidential.pdf) and uncover the flag within the metadata.
## Solucion

## Procedimiento

**1.** Abre el PDF en un lector y revisa Propiedades del documento para observar los metadatos.

**2.** También puedes consultar el campo Author con ExifTool o con Python. La cadena del autor tiene apariencia Base64.

**3.** Decodifica el valor Base64. En el PDF la cadena termina con un escape PDF \075, que representa el carácter = de relleno; una biblioteca PDF normal suele resolver ese escape al leer los metadatos.

```
import base64  
from pypdf import PdfReader  
  
pdf = PdfReader("confidential.pdf")  
autor = pdf.metadata.author  
if not autor:  
    raise SystemExit("El PDF no tiene campo Author")  
  
bandera = base64.b64decode(autor).decode("utf-8")  
print(bandera)
```
## Notas adicionales

## Referencias