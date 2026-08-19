
## Descripcion

What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.
## Solucion

Viendo el problema, la cadena esta compuesta por mezcla de letras en minuscula, mayuscula y numeros, por lo que es un sistema de decodificacion base64

Para resolverlo utilizaremos un Pipe en linux

echo "bDNhcm5fdGgzX3IwcDM1" | base64 -d

lo que dara de resultado: 
l3arn_th3_r0p35HuskyNose-academy@webshell:~$ 
## Notas adicionales

- `echo "..."`: Es el equivalente al `print()` de Python; simplemente imprime en pantalla el texto que va entre comillas.
    
- `|` (Pipe/Tubería): Redirige la salida de `echo` para que no se imprima directamente en pantalla, sino que entre directamente a la siguiente herramienta.
    
- `base64`: La herramienta nativa de Linux para procesar codificaciones Base64.
    
- `-d` (decode): La opción específica que le dice a `base64`: _"No codifiques, invierte el proceso y decodifica esto"_.
## Referencias
****