## Descripcion
This file contains more than it seems. Get the flag from [garden.jpg](https://challenge-files.cylabacademy.net/library/0b84012e7d505751ee79c0407057962df7324463d7f8495cb79f5fb2dd998d7d/garden.jpg).
## Solucion
### 1. Descripción del reto

El reto **Glory of the Garden** consiste en analizar un archivo de imagen proporcionado por el reto. Aunque el archivo parece ser solamente una imagen, contiene información adicional que permite obtener la bandera.

La pista proporcionada por el reto es:

> **What is a hex editor?**

Esto indica que es necesario analizar el contenido interno del archivo y no solamente observar la imagen.

---

### 2. Descargar el archivo

Primero se descarga el archivo proporcionado por el reto, llamado:

```
garden.jpg
```

Se puede comprobar que el archivo se encuentra en el directorio actual mediante:

```
ls
```

---

### 3. Identificar el tipo de archivo

Se utiliza el comando:

```
file garden.jpg
```

Este comando permite conocer el tipo de archivo a partir de su contenido.

**Resultado esperado:**

```
garden.jpg: JPEG image data
```

Esto confirma que el archivo corresponde a una imagen JPEG.

---

### 4. Buscar texto oculto

Como el reto indica que el archivo contiene más información de la que aparenta, se utiliza el comando `strings`:

```
strings garden.jpg
```

El comando `strings` permite mostrar las cadenas de caracteres legibles que se encuentran dentro de un archivo binario.
## Notas adicionales

## Referencias