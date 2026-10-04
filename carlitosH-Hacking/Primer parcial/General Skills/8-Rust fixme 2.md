## Descripcion
The Rust saga continues? I ask you, can I borrow that, pleeeeeaaaasseeeee?

Download the Rust code [here](https://challenge-files.cylabacademy.net/library/048c73621a97b98cde18eae5a9495279f2396cb64c65235bb310e7ad26d726ac/fixme2.tar.gz).
## Solucion
### 1. Descargar el archivo

```
wget "https://challenge-files.cylabacademy.net/library/048c73621a97b98cde18eae5a9495279f2396cb64c65235bb310e7ad26d726ac/fixme2.tar.gz"
```

Comprueba que se descargó:

```
ls
```

Deberías tener:

```
fixme2.tar.gz
```

### 2. Descomprimir

```
tar -xvf fixme2.tar.gz
```

Después:

```
ls
```

Entra a la carpeta del proyecto:

```
cd fixme2
```

y revisa su contenido:

```
ls
```

Deberías encontrar algo similar a:

```
Cargo.toml
src
```

### 3. Revisar el código

Muestra el archivo principal:

```
cat src/main.rs
```

También puedes abrirlo con:

```
nano src/main.rs
```

En este reto encontraremos errores relacionados con el código Rust que debemos corregir.

### 4. Intentar compilar

Desde la carpeta donde está `Cargo.toml`, ejecuta:

```
cargo build
```

El compilador mostrará los errores encontrados y señalará las líneas donde debemos realizar las modificaciones.

La idea es utilizar los mensajes de error de Rust para localizar cada problema.

### 5. Corregir el código

Abre nuevamente:

```
nano src/main.rs
```

Corrige los errores indicados por `cargo build`.

Después de cada modificación, vuelve a comprobar:

```
cargo build
```

Debes repetir el proceso hasta que aparezca una compilación exitosa, por ejemplo:

```
Finished `dev` profile [...]
```

### 6. Ejecutar el programa

Una vez que el código compile correctamente:

```
cargo run
```

El programa deberá ejecutar la lógica del reto y soltar la bandera
## Notas adicionales

## Referencias