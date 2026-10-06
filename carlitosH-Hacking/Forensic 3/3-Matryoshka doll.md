## Descripcion
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: [dolls.jpg](https://challenge-files.cylabacademy.net/library/370b91d430bc7ec8382557bcd2fba17a0e4e8ff86df14476a40c9f4b91276fa8/dolls.jpg)
## Solucion
# Matryoshka Doll

## 1. Descripción del reto

El reto **Matryoshka Doll** pertenece a la categoría **ForensicsMedium** y consiste en encontrar una bandera oculta dentro de varias capas de archivos.

La imagen proporcionada contiene archivos comprimidos incrustados. Cada archivo extraído contiene otra imagen, formando una estructura similar a una muñeca Matryoshka.

El objetivo es realizar la extracción de cada capa hasta encontrar el archivo `flag.txt`.

---

## 2. Descarga del archivo

Primero se descargó la imagen proporcionada por el reto:

```bash
wget "https://challenge-files.cylabacademy.net/library/370b91d430bc7ec8382557bcd2fba17a0e4e8ff86df14476a40c9f4b91276fa8/dolls.jpg" -O dolls.jpg
```

Se verificó que el archivo estuviera disponible:

```bash
ls -lh dolls.jpg
```

---

## 3. Análisis con Binwalk

Se utilizó `binwalk` para buscar archivos ocultos dentro de la imagen:

```bash
binwalk dolls.jpg
```

El análisis permitió identificar un archivo comprimido dentro de la imagen.

Para extraerlo automáticamente se utilizó:

```bash
binwalk -e dolls.jpg
```

Esto creó un directorio de extracción:

```text
_dolls.jpg.extracted/
```

Dentro de este directorio se encontró otra imagen:

```text
2_c.jpg
```

---

## 4. Extracción de las siguientes capas

Se analizó nuevamente la imagen obtenida:

```bash
binwalk -e 2_c.jpg
```

Dentro de la carpeta generada se encontró:

```text
3_c.jpg
```

Posteriormente se realizó el mismo procedimiento:

```bash
binwalk -e 3_c.jpg
```

Esto permitió obtener:

```text
4_c.jpg
```

La estructura encontrada hasta este punto fue:

```text
dolls.jpg
└── 2_c.jpg
    └── 3_c.jpg
        └── 4_c.jpg
```

Cada imagen contenía un archivo comprimido en su interior.

---

## 5. Análisis de la última imagen

Se ejecutó `binwalk` sobre `4_c.jpg`:

```bash
binwalk -e 4_c.jpg
```

El resultado mostró:

```text
79578         0x136DA         Zip archive data,
at least v1.0 to extract,
compressed size: 42,
uncompressed size: 42,
name: flag.txt
```

Esto indicó que `4_c.jpg` contenía un archivo ZIP a partir del desplazamiento `79578`, cuyo contenido era `flag.txt`.

Sin embargo, `binwalk` mostró el siguiente mensaje:

```text
WARNING: One or more files failed to extract:
either no utility was found or it's unimplemented
```

Por lo tanto, fue necesario realizar la extracción manualmente.

---

## 6. Extracción manual del archivo ZIP

Se utilizó `dd` para extraer el contenido a partir del desplazamiento indicado por Binwalk:

```bash
dd if=4_c.jpg bs=1 skip=79578 of=flag.zip
```

Después se verificó el archivo:

```bash
file flag.zip
```

El resultado indicó que se trataba de un archivo ZIP.

---

## 7. Descompresión

Se utilizó `unzip` para extraer el archivo:

```bash
unzip flag.zip
```

Esto permitió obtener:

```text
flag.txt
```

Finalmente, se mostró su contenido:

```bash
cat flag.txt
```

El contenido obtenido corresponde a la bandera del reto.
## Notas adicionales

## Referencias
