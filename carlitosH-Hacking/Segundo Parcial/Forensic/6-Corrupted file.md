## Descripcion
This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life? Download the file [here](https://challenge-files.cylabacademy.net/library/cefad24659aa422bb4e57016eda1c098a0e8f3e83fbf006b58c235ca0440cb9e/file).
## Solucion
**1.**  Ejecuta Format-Hex .\file -Count 16 en PowerShell.

**2.** Observa que los dos primeros bytes son 5C 78 (los caracteres \ y x). Después empieza FF E0. El marcador SOI FF D8 está ausente.

**3.** Escribe un JPEG reparado: añade FF D8 y conserva los bytes desde la posición 2 en adelante.

**4.** Abre repaired.jpg. La imagen muestra la bandera en texto rojo pequeño, en el centro.
## Notas adicionales

## Referencias
