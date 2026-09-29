## Descripcion
Find the flag in this [picture](https://challenge-files.cylabacademy.net/library/7ed1ce00a2228a823941d5586923914d39f3085ee0a9a432555322b8dfa9f92e/pico_img.png).
## Solucion
### 1. Descripción del reto

El reto **So Meta** pertenece a la categoría de **Forensics** y consiste en encontrar una bandera oculta dentro de una imagen.

Las pistas proporcionadas por el reto son:

> **What does meta mean in the context of files?**

> **Ever heard of metadata?**

Estas pistas indican que se deben revisar los **metadatos del archivo**, ya que pueden contener información que no es visible al abrir la imagen normalmente.

---

### 2. Descargar el archivo

Primero se descarga la imagen proporcionada por el reto.

Una vez descargada, se comprueba que el archivo se encuentre en el directorio actual mediante:

```
ls
```

---

### 3. Identificar el tipo de archivo

Se utiliza el comando:

```
file pico_img.png
```

Este comando permite identificar el formato real del archivo.

El resultado indica que se trata de una imagen, por ejemplo:

```
pico_img.png: JPEG image data
```

---

### 4. Analizar los metadatos

Para revisar la información almacenada dentro de la imagen se utiliza **ExifTool**:

```
exiftool pico_img.png
```

ExifTool permite obtener información de los metadatos de diferentes tipos de archivos, incluyendo imágenes.

Entre la información que puede mostrar se encuentran:

- Nombre del archivo.
- Tipo de archivo.
- Tamaño.
- Dimensiones de la imagen.
- Información de la cámara.
- Fecha y hora.
- Software utilizado.
- Comentarios.
- Información EXIF.

---

### 5. Buscar directamente la bandera

Como la bandera utilizada en esta plataforma comienza con:

```
academy{
```

se puede filtrar la información obtenida por ExifTool utilizando:

```
exiftool pico_img.png | grep -i academy
```

El parámetro `grep` permite buscar una cadena específica dentro de la salida del comando.

Si la bandera está almacenada directamente en alguno de los metadatos, aparecerá en el resultado con un formato similar a:

```
academy{................................}
```

---

### 6. Análisis del resultado

La información encontrada demuestra que la bandera no se encontraba necesariamente en la parte visible de la imagen, sino dentro de los **metadatos asociados al archivo**.

Los metadatos son información adicional que describe diferentes características de un archivo. En el caso de una imagen, pueden almacenar datos como el dispositivo utilizado, fecha de creación, ubicación, software y comentarios.

---

### 7. Comandos utilizados

Para documentar el procedimiento completo:

```
ls
file picture.jpg
exiftool pico_img.png
exiftool pico_img.png | grep -i academy
```
## Notas adicionales

## Referencias
