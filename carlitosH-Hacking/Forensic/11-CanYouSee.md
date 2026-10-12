## Descripcion
How about some hide and seek?

Download this file [here](https://challenge-files.cylabacademy.net/library/9b029ae1f6eeb888f00d61f70ef1223afce75f409a25b0076838b9af310b66c3/unknown.zip).
## Solucion
## 1. Descargar el archivo

Abre una terminal en Kali Linux y crea una carpeta para organizar el reto:

```
mkdir CanYouSee
cd CanYouSee
```

Descarga el archivo:

```
wget "https://challenge-files.cylabacademy.net/library/9b029ae1f6eeb888f00d61f70ef1223afce75f409a25b0076838b9af310b66c3/unknown.zip"
```

Comprueba que se haya descargado correctamente:

```
file unknown.zip
ls -lh unknown.zip
```

## 2. Descomprimir el archivo

Extrae su contenido:

```
unzip unknown.zip
```

Después, lista los archivos:

```
ls -lah
```

Si aparece una imagen con un nombre como `ukn_reality.jpg`, esa será la que analizaremos.

## 3. Analizar los metadatos de la imagen
Ejecuta el análisis sobre la imagen extraída:

```
exiftool ukn_reality.jpg
```

Busca el campo `Attribution URL`. Contendrá una cadena que parece aleatoria, pero está codificada en Base64. La pista del reto consiste precisamente en revisar la información de la imagen y detectar ese valor inusual.
## 4. Decodificar la cadena

Puedes extraer directamente el valor con este comando:

```
exiftool -AttributionURL -s3 ukn_reality.jpg
```

Copia el valor obtenido y decodifícalo:

```
echo 'YWNhZGVteXtNRTc0RDQ3QV9ISUREM05fOTI3MTgzYjN9Cg==' | base64 -d
```
## Notas adicionales

## Referencias