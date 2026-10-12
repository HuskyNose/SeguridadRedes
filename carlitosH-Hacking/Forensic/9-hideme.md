## Descripcion
Every file gets a flag. The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye [here](https://challenge-files.cylabacademy.net/library/afab2dc0b8164303df06666c7b574103668443cba057e14f9d6683ce67665bda/flag.png).
## Solucion
## 1. Descargar la imagen

Crea una carpeta y descarga el archivo:

```
mkdir hideme
cd hideme

wget "https://challenge-files.cylabacademy.net/library/afab2dc0b8164303df06666c7b574103668443cba057e14f9d6683ce67665bda/flag.png"
```

Comprueba el tipo de archivo y sus propiedades:

```
file flag.png
ls -lh flag.png
```

## 2. Revisar los metadatos

Ejecuta ExifTool para revisar la información del archivo:

```
exiftool flag.png
```

Analiza la imagen:

```
binwalk flag.png
```

Busca firmas de archivos como ZIP, datos comprimidos u otros formatos reconocibles. Si aparecen archivos adicionales dentro de la imagen, el siguiente paso será extraerlos.

## 3. Extraer los archivos ocultos

Ejecuta el siguiente comando:

```
binwalk -e flag.png
```

Si la extracción falla por permisos o por la configuración de tu versión de Binwalk, prueba:

```
binwalk --run-as=root -e flag.png
```

Se creará una carpeta llamada `_flag.png.extracted`. Revisa su contenido:

```
ls -la _flag.png.extracted
```

Entre los archivos extraídos, deberías encontrar un directorio llamado `secret`, que contiene otra imagen llamada `flag.png`.
## 4. Abrir la imagen que contiene la bandera

Ejecuta:

```
file _flag.png.extracted/secret/flag.png
```

Después, abre la imagen:

```
xdg-open _flag.png.extracted/secret/flag.png
```
## Notas adicionales
`binwalk`
```
sudo apt update
sudo apt install binwalk
```
## Referencias
