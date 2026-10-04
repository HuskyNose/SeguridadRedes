## Descripcion
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!

Download the Rust code [here](https://challenge-files.cylabacademy.net/library/b9cfc84c442958b8ac848ddc0692bed9ef01a15877b8d37f36afbe68b5849acc/fixme1.tar.gz).
## Solucion
### 1. Descargar el archivo

```
wget "https://challenge-files.cylabacademy.net/library/b9cfc84c442958b8ac848ddc0692bed9ef01a15877b8d37f36afbe68b5849acc/fixme1.tar.gz"
```

### 2. Descomprimirlo

```
tar -xvf fixme1.tar.gz
```

Después revisamos los archivos:

```
ls
```

Normalmente encontraremos una carpeta del proyecto.

Puedes entrar a ella con:

```
cd fixme1
```

y comprobar su contenido:

```
ls
```

Deberías encontrar archivos relacionados con Rust, principalmente:

```
Cargo.toml
src/
```

### 3. Revisar el código

Entramos al directorio `src`:

```
cd src
```

y mostramos el código:

```
cat main.rs
```

También puedes utilizar:

```
nano main.rs
```

Aquí encontraremos los errores de sintaxis que debemos corregir.

### 4. Compilar el programa

Regresamos a la carpeta principal del proyecto:

```
cd ..
```

y ejecutamos:

```
cargo build
```

Rust indicará los errores encontrados y normalmente señalará **el archivo y número de línea** donde se encuentra cada problema.

### 5. Corregir los errores

Abrimos nuevamente el archivo:

```
nano src/main.rs
```

Se corrigen los errores de sintaxis indicados por el compilador.

Una vez realizada una corrección, volvemos a ejecutar:

```
cargo build
```

Si todavía existen errores, Rust mostrará los siguientes que debemos corregir.

Este proceso se repite hasta obtener una compilación exitosa.

### 6. Ejecutar el programa

Cuando `cargo build` termine correctamente, ejecutamos:

```
cargo run
```

El programa debería ejecutarse y mostrar la bandera
## Notas adicionales

## Referencias