## Descripcion
The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log. Download the encoded data here: [Logs Data](https://challenge-files.cylabacademy.net/library/e6fc51b98dd61381c5cd54dc836c8344fb475f17728f2095969e3a0f401ea195/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial .
## Solucion

**1.** Decodifica el contenido completo de logs.txt como Base64 y guarda el resultado como decoded.png.

**2.** Abre decoded.png con Fotos o Paint. Amplía la parte inferior de la imagen.

**3.** Copia la secuencia hexadecimal que aparece en la franja inferior.

**4.** Convierte el hexadecimal a bytes y después a texto UTF-8. El texto resultante ya contiene la bandera completa.
## Notas adicionales

## Referencias