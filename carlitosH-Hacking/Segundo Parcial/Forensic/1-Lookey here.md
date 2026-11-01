## Descripcion
Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it. Download the data [here](https://challenge-files.cylabacademy.net/library/1461fca1c694c5c9ca0fb1fe427c36f56d80f5f23eb617a51c95fe1b6ca5ed83/anthem.flag.txt)
## Solucion

El reto consiste en buscar una cadena que no pertenece al texto normal y está insertada en medio del archivo.
```
from pathlib import Path  
import re  
  
texto = Path("anthem.flag.txt").read_text(encoding="utf-8")  
coincidencia = re.search(r"academy\{[^}]+\}", texto)  
  
if coincidencia:  
    print(coincidencia.group(0))  
else:  
    print("No se encontró una bandera")
```
## Notas adicionales

## Referencias
