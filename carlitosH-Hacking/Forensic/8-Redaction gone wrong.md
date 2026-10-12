## Descripcion
Now you DON’T see me. This [report](https://challenge-files.cylabacademy.net/library/455e6e9581a9272cf0cd6a8f2da0a7cdcfefdb52dc7a7f9c09a27705e2c94103/Financial_Report_for_ABC_Labs.pdf) has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?
## Solucion
## 1. Descargar el archivo en Kali Linux

Crea una carpeta para el reto y descarga el reporte:

```
mkdir redaction_gone_wrong
cd redaction_gone_wrong

wget "https://challenge-files.cylabacademy.net/library/455e6e9581a9272cf0cd6a8f2da0a7cdcfefdb52dc7a7f9c09a27705e2c94103/Financial_Report_for_ABC_Labs.pdf"
```

Comprueba que el archivo se haya descargado correctamente:

```
file Financial_Report_for_ABC_Labs.pdf
```

## 2. Extraer el texto del PDF

Primero, utiliza `pdftotext`, una herramienta que permite extraer el texto de documentos PDF aunque algunas partes estén visualmente cubiertas.


Extrae el texto a un archivo:

```
pdftotext -layout Financial_Report_for_ABC_Labs.pdf reporte.txt
```
pdftotext -layout Financial_Report_for_ABC_Labs.pdf reporte.txt


Buscar palabras relacionadas con claves y credenciales:

```
grep -inE 'key|secret|password|token|flag|academy' reporte.txt
```
## Notas adicionales
pdftotext
```
sudo apt update
sudo apt install poppler-utils
```
## Referencias
