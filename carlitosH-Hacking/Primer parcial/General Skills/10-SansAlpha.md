## Descripcion
The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols. `ssh -p 18701 ctf-player@xebec.cylabacademy.net`

Use password: `647e170e`
## Solucion
## 1. Conectarte por SSH

Ejecuta:

```
ssh -p 18701 ctf-player@xebec.cylabacademy.net
```

Cuando pida contraseña:

```
647e170e
```

Una vez dentro aparecerá algo parecido a:

```
SansAlpha$
```

Si intentas:

```
ls
```

el servidor rechazará las letras:

```
SansAlpha: Unknown character detected
```

Por eso necesitamos construir los comandos **sin escribir ninguna letra**.

---

# 2. Obtener letras mediante un error de Bash

La solución consiste en provocar un error utilizando únicamente símbolos.

Escribe:

```
_1="$(- 2>&1)"
```

Aquí no estamos escribiendo ninguna letra como comando. El `-` provoca un error y `2>&1` redirige el mensaje de error.

Después, podemos mostrar el contenido de `_1` ejecutándolo como expansión:

```
"$_1"
```

Obtendrás algo parecido a:

```
bash: bash: -: command not found
```

Ese mensaje es muy importante porque **ahora tenemos letras disponibles dentro de una variable**. Esta técnica es precisamente la clave utilizada para resolver SansAlpha.

---

# 3. Construir `cat`

Necesitamos las letras:

```
c
a
t
```

Podemos extraer caracteres individuales de `_1` mediante:

```
${variable:posición:cantidad}
```

Por ejemplo:

```
${_1:9:1}
```

extrae un carácter de la variable.

Para construir `cat`:

```
_2="${_1:9:1}${_1:1:1}${_1:19:1}"
```

Ahora `_2` contiene:

```
cat
```

La ventaja es que **nosotros nunca escribimos `cat` directamente**; Bash construye la palabra usando los caracteres que ya existen en `_1`.

---

# 4. Buscar el archivo

Ahora podemos utilizar `cat`, pero todavía necesitamos encontrar el archivo.

Una forma sencilla es utilizar los comodines de Bash.

Por ejemplo:

```
**/*
```

Esto permite expandir rutas utilizando `*`, sin tener que escribir nombres con letras.

En el entorno del reto se encuentra un directorio llamado:

```
blargh
```

y dentro de él está:

```
flag.txt
```

Los writeups del reto confirman que la ruta relevante es `blargh/flag.txt`.

---

# 5. Leer la flag

Como ya tenemos `cat` almacenado en `_2`, podemos ejecutar:

```
$_2 **/*
```

La expansión de `**/*` encuentra los archivos y `cat` intenta mostrar su contenido.
## Notas adicionales

## Referencias
