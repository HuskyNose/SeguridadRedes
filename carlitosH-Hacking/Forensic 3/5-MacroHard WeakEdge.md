## Descripcion
I've hidden a flag in this file. Can you find it? [Forensics_is_fun.pptm](https://challenge-files.cylabacademy.net/library/ef35dfe613527d28fe872d94179b53bc1a0497ddecf57e51d160c910be3a8e8a/Forensics_is_fun.pptm)
## Solucion
# MacroHard WeakEdge

**Categoría:** Forensics  
**Dificultad:** Medium  
**Autor:** madStackspicoCTF 2021

## 1. Descripción del reto

Se proporciona un archivo llamado `Forensics_is_fun.pptm` que contiene una bandera oculta. El objetivo es analizar el archivo y encontrar la información escondida dentro de él.

## 2. Identificación del archivo

Primero se verificó el tipo de archivo utilizando el comando `file`:

```bash
file Forensics_is_fun.pptm
```

El archivo corresponde a una presentación de Microsoft PowerPoint.

## 3. Extracción del archivo PPTM

Los archivos `.pptm` utilizan internamente una estructura basada en archivos ZIP, por lo que se puede extraer su contenido utilizando `unzip`:

```bash
unzip Forensics_is_fun.pptm
```

Después de la extracción se generaron diferentes carpetas y archivos correspondientes a la estructura interna de la presentación.

## 4. Búsqueda de archivos ocultos

Se utilizó el comando `find` para localizar un archivo llamado `hidden`:

```bash
find . -name hidden
```

El resultado mostró:

```text
./ppt/slideMasters/hidden
```

Este archivo se encontraba dentro de la carpeta `ppt/slideMasters`.

## 5. Lectura del archivo oculto

Se utilizó `cat` para visualizar su contenido:

```bash
cat ppt/slideMasters/hidden
```

El contenido encontrado tenía caracteres separados por espacios:

```text
Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q
```

Por su formato, se identificó que se trataba de información codificada en Base64.

## 6. Eliminación de espacios

Antes de decodificar la información fue necesario eliminar los espacios entre los caracteres.

Se utilizó:

```bash
cat ppt/slideMasters/hidden | tr -d ' '
```

El resultado fue:

```text
ZmxhZzogcGljb0NURntEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ
```

## 7. Decodificación de Base64

Finalmente, se utilizó `base64 -d` para decodificar la cadena:

```bash
cat ppt/slideMasters/hidden | tr -d ' ' | base64 -d
```

El resultado fue:

```text
flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5}
```

## 8. Bandera obtenida

La bandera
## Notas adicionales

## Referencias
