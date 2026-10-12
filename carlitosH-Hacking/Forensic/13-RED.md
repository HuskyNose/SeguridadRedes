## Descripcion
RED, RED, RED, RED Download the image: [red.png](https://challenge-files.cylabacademy.net/library/fefcf06050d98347e1585e5cb9f2940967f82e0b89c591966473c752de9f3aba/red.png)
## Solucion
## 1. Descargar la imagen

Crea una carpeta para el reto y descarga el archivo:

```
mkdir RED
cd RED

wget "https://challenge-files.cylabacademy.net/library/fefcf06050d98347e1585e5cb9f2940967f82e0b89c591966473c752de9f3aba/red.png"
```

Comprueba el tipo y tamaño del archivo:

```
file red.png
ls -lh red.png
```

## 2. Examinar los metadatos
Ejecuta:

```
exiftool red.png
```

Revisa si aparece algún campo inusual, como comentarios o información adicional.

También puedes inspeccionar los datos internos del PNG:

```
binwalk red.png
```

Esto permite buscar estructuras o archivos incrustados en la imagen.

## 3. Encontrar la pista oculta

Ejecuta:

```
strings red.png
```

Busca un poema en los datos del archivo. También puedes verlo con:

```
exiftool red.png
```

El poema contiene una pista formada por la primera letra de cada línea. Al leerlas verticalmente se obtiene:

```
CHECKLSB
```

Esto significa que debemos revisar el LSB (Least Significant Bit), es decir, el bit menos significativo de los canales de color de la imagen.

## 4. Instalar y ejecutar zsteg
Analiza la imagen:

```
zsteg red.png
```

Busca una línea similar a esta:

```
b1,rgba,lsb,xy .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="
```

El resultado es una cadena codificada en Base64.

## 5. Decodificar la bandera

Copia la cadena encontrada y ejecuta:

```
echo 'YWNhZGVteXtyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==YWNhZGVteXtyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==YWNhZGVteXtyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==YWNhZGVteXtyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==' | base64 -d

```

## Notas adicionales

## Referencias
