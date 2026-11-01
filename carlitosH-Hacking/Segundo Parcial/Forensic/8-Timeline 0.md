## Descripcion
Can you find the flag in this disk image? Wrap what you find in the academy{} flag format. Download the disk image [here](https://challenge-files.cylabacademy.net/library/bf9a20c350075c5863371e078daee1d570d4062902edc8a4a042e02a7cebf161/partition4.img.gz)
## Solucion
### 1. Analizar la imagen forense

- Trabajar con `partition4.img`.
    
- Revisar el sistema de archivos y extraer su contenido mediante `pytsk3`.
    
- Generar un timeline con las fechas de acceso, modificación, creación y cambio de metadatos de los archivos.
    

### 2. Revisar el timeline generado

- Abrir `timeline.csv`.
    
- Buscar fechas que no coincidan con el comportamiento normal del sistema.
    
- Identificar archivos con marcas de tiempo sospechosas.
    
- Prestar especial atención a `/bin/bcab`, `/root/.ash_history` y `/var/log/messages`.
    

### 3. Investigar el archivo sospechoso `/bin/bcab`

- Localizarlo dentro de la imagen.
    
- Extraer su contenido.
    
- Revisar si contiene texto codificado.
    
- En nuestro caso encontramos:
    

```
NzFtMzExbjNfMHU3MTEzcl9oM3JfNDNhMmU3YWYK
```

### 4. Decodificar el contenido

- Identificar la codificación utilizada.
    
- Decodificar la cadena en Base64.
    
- Analizar el resultado y reconocer posibles sustituciones de caracteres mediante leetspeak.
    

El resultado que obtuvimos fue:

```
71m311n3_0u7113r_h3r_43a2e7af
```


## Notas adicionales

## Referencias
