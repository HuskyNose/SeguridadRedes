## Descripcion
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?

Download the suspicious file [here](https://challenge-files.cylabacademy.net/library/00e64c4ab0a092f8fef0d856d022560edd3e465c62dce1b270d764a99a9c4e1a/flag2of2-final.pdf).
## Solucion
## 1. Descargar el archivo

Crea una carpeta de trabajo y descarga el archivo proporcionado:

```
mkdir SecretPolyglot
cd SecretPolyglot

wget "https://challenge-files.cylabacademy.net/library/00e64c4ab0a092f8fef0d856d022560edd3e465c62dce1b270d764a99a9c4e1a/flag2of2-final.pdf"
```

Comprueba que el archivo se haya descargado correctamente:

```
ls -lh flag2of2-final.pdf
```

## 2. Identificar el tipo de archivo

Aunque la extensión sea `.pdf`, no debemos asumir que contiene únicamente un documento PDF.

Ejecuta:

```
file flag2of2-final.pdf
```

Después, revisa las firmas y estructuras internas:

```
binwalk flag2of2-final.pdf
```

El comando `file` identifica el formato a partir de la estructura del archivo, mientras que `binwalk` busca firmas de otros formatos incrustados.

## 3. Extraer los archivos incrustados

Si `binwalk` detecta una firma PNG además de la estructura PDF, intenta extraerla automáticamente:

```
binwalk -e flag2of2-final.pdf
```

Revisa los archivos generados:

```
find . -maxdepth 3 -type f
```

Si aparece una carpeta como `_flag2of2-final.pdf.extracted`, inspecciona su contenido:

```
ls -lah _flag2of2-final.pdf.extracted
```

Si Binwalk no extrae los datos, no significa que no existan. Puedes revisar el archivo con `xxd` y buscar firmas PNG, cuya secuencia inicial característica es `89 50 4e 47 0d 0a 1a 0a`.

## 4. Revisar el PDF y la imagen

Extrae el texto del PDF:

```
pdftotext -layout flag2of2-final.pdf documento.txt
cat documento.txt
```


## 5. Abrir el archivo con las dos extensiones

La clave del reto es que no necesitas extraer un archivo con Binwalk necesariamente. El mismo archivo puede abrirse de dos maneras.

Primero, comprueba el formato real:

```
file flag2of2-final.pdf
```



Ahora crea una copia con extensión PNG:

```
cp flag2of2-final.pdf flag2.png
```

Abre la imagen:

```
xdg-open flag2.png
```

En la imagen deberías ver la primera parte de la bandera

Por otro lado, abre el archivo original como PDF

## Notas adicionales

## Referencias
