## Descripcion
Files can always be changed in a secret way. Can you find the flag? [cat.jpg](https://challenge-files.cylabacademy.net/library/c585b4adbdaa06f409db7bf5012c2e58e9aab24669764a5f1cf0f9ce0d60dcfd/cat.jpg)

## Solucion
### Paso 1. Descargar el archivo

Se descargó la imagen `cat.jpg` desde el enlace proporcionado por la plataforma. Posteriormente, se creó un directorio de trabajo para organizar los archivos del reto.

```bash
mkdir information
cd information
wget "https://challenge-files.cylabacademy.net/library/c585b4adbdaa06f409db7bf5012c2e58e9aab24669764a5f1cf0f9ce0d60dcfd/cat.jpg"
```

### Paso 2. Verificar el archivo

Se utilizó el comando `file` para identificar el tipo de archivo descargado y comprobar que correspondiera a una imagen JPEG.

```bash
file cat.jpg
```

### Paso 3. Analizar los metadatos

Se utilizó la herramienta ExifTool para examinar los metadatos de la imagen.

```bash
exiftool cat.jpg
```

Al revisar la información obtenida, se identificó el campo `License`, que contenía una cadena codificada en Base64. Esto indicó que era necesario decodificar su contenido para recuperar el mensaje oculto.

### Paso 4. Decodificar la información

Se copió el valor encontrado en el campo `License` y se utilizó el comando `base64 -d` para convertirlo a texto legible.

```bash
echo "YWNhZGVteXt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9" | base64 -d

```
### Paso 5. Adaptar la bandera

La bandera recuperada originalmente tenía el prefijo `picoCTF`. Como la plataforma solicita el formato `academy{XXXXX}`, se adaptó el prefijo al formato requerido, conservando el contenido interno de la bandera.

**Bandera final:** `academy{the_m3tadata_1s_modified}`
## Notas adicionales

## Referencias
