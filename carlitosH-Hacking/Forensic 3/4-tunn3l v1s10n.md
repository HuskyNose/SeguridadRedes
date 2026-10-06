## Descripcion
We found this file. Recover the flag. [tunn3l_v1s10n](https://challenge-files.cylabacademy.net/library/3b5add918cb4cf98fa62ef4e05eb8c55c6c9ae547a939c6be992ee3aa656ee69/tunn3l_v1s10n)
## Solucion
# tunn3l v1s10n

## 1. Identificación del archivo

Primero se verificó el tipo de archivo utilizando `file`:

```bash
file tunn3l_v1s10n
```

El resultado indicó:

```text
tunn3l_v1s10n: data
```

Esto indica que el sistema no pudo identificar correctamente el archivo mediante su extensión o estructura.

---

## 2. Análisis de los primeros bytes

Se revisó la cabecera del archivo con `xxd`:

```bash
xxd -g 1 -l 64 tunn3l_v1s10n
```

Se obtuvo:

```text
00000000: 42 4d 8e 26 2c 00 00 00 00 00 ba d0 00 00 ba d0
00000010: 00 00 6e 04 00 00 32 01 00 00 01 00 18 00 00 00
```

Los primeros dos bytes son:

```text
42 4d
```

Estos corresponden a la firma `BM`, utilizada por los archivos **BMP**.

Por lo tanto, se determinó que el archivo era un BMP cuya cabecera estaba modificada o corrupta.

---

## 3. Obtención de información del BMP

Se utilizó `exiftool`:

```bash
exiftool tunn3l_v1s10n
```

Entre los datos obtenidos se encontraron:

```text
File Type        : BMP
Image Width      : 1134
Image Height     : 306
Bit Depth        : 24
Compression      : None
Image Length     : 2893400
```

El ancho de la imagen era de **1134 píxeles**, mientras que la altura indicada era de **306 píxeles**.

Al revisar la estructura de la cabecera, se observaron valores incorrectos que impedían interpretar correctamente la imagen.

---

## 4. Identificación de los valores corruptos

En un archivo BMP estándar:

- En el desplazamiento `0x0A` se encuentra la posición donde comienzan los datos de los píxeles.
    
- En `0x0E` se encuentra el tamaño de la cabecera DIB.
    
- En `0x16` se encuentra la altura de la imagen.
    

En este archivo aparecían valores incorrectos:

```text
Offset 0x0A → BA D0 00 00
Offset 0x0E → BA D0 00 00
Offset 0x16 → 32 01 00 00
```

El valor `32 01 00 00` corresponde a una altura de:

```text
0x132 = 306
```

---

## 5. Corrección de la cabecera

Primero se realizó una copia para conservar el archivo original:

```bash
cp tunn3l_v1s10n tunn3l_v1s10n_fixed
```

Después se corrigieron los valores de la cabecera utilizando Python.

```bash
python3 -c "f=open('tunn3l_v1s10n_fixed','r+b'); f.seek(10); f.write(bytes.fromhex('36000000')); f.seek(14); f.write(bytes.fromhex('28000000')); f.seek(22); f.write(bytes.fromhex('52030000')); f.close()"
```

Los cambios realizados fueron:

|Offset|Valor original|Valor corregido|Función|
|---|---|---|---|
|`0x0A`|`BA D0 00 00`|`36 00 00 00`|Inicio de los datos de píxeles|
|`0x0E`|`BA D0 00 00`|`28 00 00 00`|Tamaño de la cabecera DIB|
|`0x16`|`32 01 00 00`|`52 03 00 00`|Altura de la imagen|

El valor `52 03 00 00` corresponde a:

```text
0x352 = 850
```

Por lo tanto, la imagen queda con dimensiones:

```text
1134 × 850
```

---

## 6. Verificación de la cabecera

Se verificaron nuevamente los primeros bytes:

```bash
xxd -g 1 -l 32 tunn3l_v1s10n_fixed
```

La cabecera corregida debe comenzar aproximadamente de esta manera:

```text
00000000: 42 4d 8e 26 2c 00 00 00 00 00 36 00 00 00 28 00
00000010: 00 00 6e 04 00 00 52 03 00 00 01 00 18 00 00 00
```

También se puede comprobar nuevamente la información de la imagen:

```bash
exiftool tunn3l_v1s10n_fixed
```

Ahora debe mostrar una altura de aproximadamente:

```text
Image Width  : 1134
Image Height : 850
```

---

## 7. Visualización de la imagen

Finalmente, se abrió la imagen corregida:

```bash
xdg-open tunn3l_v1s10n_fixed
```

La imagen pudo visualizarse correctamente y permitió recuperar la información oculta.

Es importante mencionar que utilizar:

```bash
strings tunn3l_v1s10n_fixed
```

no permite encontrar directamente la bandera, ya que en este reto la información se encuentra **representada visualmente dentro de la imagen**, no almacenada como texto plano.

## Notas adicionales

## Referencias