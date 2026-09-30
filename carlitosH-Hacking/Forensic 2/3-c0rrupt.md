## Descripcion
## Descargar el archivo

Primero se descarga el archivo proporcionado por el reto:

```
wget "https://challenge-files.cylabacademy.net/library/8388ecc430588d15064755583476bec46e23d42a6d8de6e8995c19e40f2e4c58/c0rrupt-mystery" -O c0rrupt-mystery
```

Se comprueba que el archivo exista:

```
ls -l c0rrupt-mystery
```

---

## 3. Identificar el tipo de archivo

Se utiliza el comando `file`:

```
file c0rrupt-mystery
```

El archivo no es identificado correctamente como una imagen porque su encabezado está corrupto.

Por lo tanto, se procede a analizar su contenido hexadecimal.

---

## 4. Analizar el archivo en hexadecimal

Se utiliza `xxd`:

```
xxd -g 1 c0rrupt-mystery | head
```

Se obtiene:

```
00000000: 89 65 4e 34 0d 0a b0 aa 00 00 00 0d 43 22 44 52
00000010: 00 00 06 6a 00 00 04 47 08 02 00 00 00 7c 8b ab
00000020: 78 00 00 00 01 73 52 47 42 00 ae ce 1c e9 00 00
00000030: 00 04 67 41 4d 41 00 00 b1 8f 0b fc 61 05 00 00
```

Los primeros bytes son:

```
89 65 4e 34 0d 0a b0 aa
```

Estos bytes son sospechosos porque los archivos PNG tienen una firma conocida:

```
89 50 4e 47 0d 0a 1a 0a
```

Por lo tanto, se determina que el archivo originalmente es un **PNG**, pero su encabezado está corrupto.

---

## 5. Identificar las partes corruptas

Además del encabezado, se encuentran otras partes dañadas.

### Firma PNG

Archivo original:

```
89 65 4e 34 0d 0a b0 aa
```

Firma correcta:

```
89 50 4e 47 0d 0a 1a 0a
```

---

### Chunk IHDR

Después de la firma aparecen los bytes:

```
43 22 44 52
```

Estos deberían corresponder al chunk `IHDR`.

La representación hexadecimal correcta de `IHDR` es:

```
49 48 44 52
```

Por lo tanto:

```
43 22 44 52
        ↓
49 48 44 52
```

---

### Chunk pHYs

Más adelante se encuentra:

```
70 48 59 73 aa 00 16 25 00 00 16 25
```

La estructura corresponde al chunk `pHYs`.

Se detecta que el primer valor de resolución está corrupto:

```
aa 00 16 25
```

y debe ser:

```
00 00 16 25
```

Por lo tanto:

```
aa 00 16 25
        ↓
00 00 16 25
```

---

### Chunk IDAT

En la dirección `0x50` se encuentra:

```
52 24 f0 aa aa ff a5 ab 44 45 54 78 5e
```

Los bytes:

```
44 45 54
```

representan:

```
DET
```

Sin embargo, los datos de imagen de un PNG utilizan el chunk:

```
IDAT
```

Su representación hexadecimal es:

```
49 44 41 54
```

Por lo tanto, se corrige:

```
44 45 54
        ↓
49 44 41 54
```

También se corrige la longitud asociada al chunk para obtener la estructura válida:

```
aa aa ff a5 ab
        ↓
00 00 ff a5 49
```

---

## 6. Crear una copia del archivo

Antes de modificarlo se crea una copia:

```
cp c0rrupt-mystery mystery.png
```

De esta forma se conserva el archivo original.

---

## 7. Reparar el archivo mediante Python

Como no es necesario utilizar un editor hexadecimal, se puede modificar directamente el archivo mediante Python.

Se ejecuta:

```
python3 -c "p='mystery.png'; d=bytearray(open(p,'rb').read()); d[0:8]=bytes.fromhex('89 50 4e 47 0d 0a 1a 0a'); d[12:16]=b'IHDR'; d[0x50:0x58]=bytes.fromhex('52 24 f0 00 00 ff a5 49'); d[0x58:0x5c]=b'IDAT'; open(p,'wb').write(d)"
```

Este comando modifica directamente los bytes corruptos:

```
Firma PNG:
89 65 4e 34 0d 0a b0 aa
↓
89 50 4e 47 0d 0a 1a 0a
```

y:

```
IHDR:
43 22 44 52
↓
49 48 44 52
```

Además, corrige la estructura del chunk `IDAT`.

---

## 8. Verificar el archivo reparado

Se utiliza nuevamente `file`:

```
file mystery.png
```

Ahora el archivo debe ser reconocido como una imagen PNG.

También se puede utilizar `pngcheck` para comprobar la estructura interna del archivo:

```
sudo apt install pngcheck
```

Después:

```
pngcheck -v mystery.png
```

Esta herramienta permite comprobar los diferentes chunks del PNG, como:

```
IHDR
sRGB
gAMA
pHYs
IDAT
IEND
```

Si no aparecen errores críticos, significa que la estructura del PNG fue reparada correctamente.

---

## 9. Visualizar la imagen

Finalmente se abre la imagen:

```
xdg-open mystery.png
```

La imagen recuperada contiene la bandera del reto.

---

## 10. Resultado

La bandera obtenida es:

```
academy{c0rrupt10n_1847995}
```
## Solucion

## Notas adicionales
