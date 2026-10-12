## Descripcion
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?

You can download the challenge files here:

- [challenge.zip](https://challenge-files.cylabacademy.net/library/28f7fa0ca184e19eeea049b6013ccedc68033a4b7e2e396207048882fd30895e/challenge.zip)
## Solucion
## 1. Descargar y descomprimir el archivo

Crea una carpeta de trabajo y descarga `challenge.zip`:

```
mkdir scan_surprise
cd scan_surprise

wget "https://challenge-files.cylabacademy.net/library/28f7fa0ca184e19eeea049b6013ccedc68033a4b7e2e396207048882fd30895e/challenge.zip"
```

Comprueba el archivo:

```
file challenge.zip
```

Descomprime su contenido:

```
unzip challenge.zip
```
## 2. Inspeccionar los archivos extraídos

Lista los archivos y directorios:

```
ls -lah
find . -maxdepth 3 -type f
```

El reto original utiliza un archivo comprimido que contiene numerosos archivos de imagen pequeños. Esos archivos representan partes de la bandera, por lo que conviene inspeccionar primero su estructura antes de intentar reconstruirla.

## 3. Localizar la imagen de la bandera

Busca los archivos PNG dentro de la carpeta extraída:

```
find . -type f -iname "*.png"
```

En el reto original, la imagen relevante se encuentra dentro de la estructura `home/ctf-player/drop-in/`. Entra al directorio correspondiente:

```
cd home/ctf-player/drop-in
ls -lah
```

Comprueba el tipo de archivo:

```
file flag.png
```

## 4. Leer la bandera mediante el código QR

La imagen contiene un código QR

```
xdg-open flag.png
```

Ejecuta el lector de códigos QR:

```
zbarimg flag.png
```
## Notas adicionales
 `unzip`

```
sudo apt update
sudo apt install unzip
```

`zbar-tools`:

```
sudo apt update
sudo apt install zbar-tools
