## Descripcion
This is a really weird text file. Can you find the flag? Get the flag from [TXT](https://challenge-files.cylabacademy.net/library/a5d365fedad883763fb28c78e25a1765220bef6501848c84f2a7a7adf74d83cd/flag.txt).
## Solucion
## 1. Descarga del archivo

Primero se descargó el archivo proporcionado por el reto utilizando `wget`:

```
wget "https://challenge-files.cylabacademy.net/library/a5d365fedad883763fb28c78e25a1765220bef6501848c84f2a7a7adf74d83cd/flag.txt"
```

Posteriormente se verificó que el archivo estuviera presente mediante:

```
ls -l flag.txt
```

## 2. Identificación del tipo de archivo

Se utilizó el comando `file` para determinar el tipo real del archivo:

```
file flag.txt
```

Aunque el archivo tenía la extensión `.txt`, el comando permitió identificar que su contenido correspondía realmente a una **imagen PNG**.

Esto demuestra que la extensión de un archivo no necesariamente indica su formato real. Los sistemas operativos y herramientas como `file` también pueden utilizar información interna del archivo, conocida como **firma del archivo (file signature)** o **magic bytes**, para determinar su tipo.

## 3. Análisis de los primeros bytes

Para comprobar la firma del archivo se utilizaron los siguientes comandos:

```
xxd -l 16 flag.txt
```

o:

```
hexdump -C -n 16 flag.txt
```

Los primeros bytes corresponden a la firma característica de un archivo PNG:

```
89 50 4E 47 0D 0A 1A 0A
```

Por lo tanto, se confirmó que `flag.txt` no era realmente un archivo de texto, sino una imagen PNG cuyo nombre había sido modificado.

## 4. Cambio de extensión

Después de identificar el formato real, se cambió la extensión del archivo:

```
mv flag.txt flag.png
```

Posteriormente se comprobó nuevamente el tipo:

```
file flag.png
```

Finalmente, la imagen pudo abrirse utilizando el visor gráfico del sistema:

```
xdg-open flag.png
```

## 5. Obtención de la flag

Al abrir la imagen se pudo visualizar la información contenida en ella y obtener la flag solicitada por el reto.

La respuesta debía utilizar el formato indicado por la plataforma:

```
academy{now_you_know_about_extensions}
```
## Notas adicionales

## Referencias
