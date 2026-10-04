## Descripcion
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!

Download the Rust code [here](https://challenge-files.cylabacademy.net/library/6df8b7779faf29e53f515922041d99bc26381a332ca090c291ba20577ac7cf92/fixme3.tar.gz).
## Solucion
### 1. Descargar el archivo

En el enlace **“here”** del reto, copia la URL y utiliza:

```
wget "URL_DEL_ARCHIVO"
```

Por ejemplo, si el archivo se llama `fixme3.tar.gz`:

```
wget "https://challenge-files.cylabacademy.net/.../fixme3.tar.gz"
```

Comprueba que esté descargado:

```
ls
```

### 2. Descomprimir

```
tar -xvf fixme3.tar.gz
```

Después:

```
ls
```

Entra en la carpeta del proyecto:

```
cd fixme3
```

Comprueba su contenido:

```
ls
```

Normalmente encontrarás:

```
Cargo.toml
src
```

### 3. Revisar el código

Muestra el archivo principal:

```
cat src/main.rs
```

O ábrelo para editarlo:

```
nano src/main.rs
```

### 4. Compilar

Desde la carpeta donde se encuentra `Cargo.toml`, ejecuta:

```
cargo build
```

Rust mostrará los errores de sintaxis indicando la línea donde se encuentra cada problema.

Por ejemplo:

```
error: ...
 --> src/main.rs:XX:XX
```

Esto nos permite localizar los errores que debemos corregir.

### 5. Corregir los errores

Abre el archivo:

```
nano src/main.rs
```

Realiza las correcciones indicadas por el compilador.

Después guarda el archivo y vuelve a ejecutar:

```
cargo build
```

Continúa corrigiendo los errores hasta que el programa compile correctamente.
## Notas adicionales

## Referencias
