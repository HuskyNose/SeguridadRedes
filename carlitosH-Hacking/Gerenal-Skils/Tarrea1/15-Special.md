## Descripcion
Don't power users get tired of making spelling mistakes in the shell? Not anymore! Enter Special, the Spell Checked Interface for Affecting Linux. Now, every word is properly spelled and capitalized... automatically and behind-the-scenes! Be the first to test Special in beta, and feel free to tell us all about how Special streamlines every development process that you face. When your co-workers see your amazing shell interface, just tell them: That's Special (TM)

Start your instance to see connection details.

`ssh -p 52211 [ctf-player@saturn.picoctf.net](mailto:ctf-player@saturn.picoctf.net)`

The password is `d137d16e`
## Solucion

## 1. Descripción

El reto **Special**, desarrollado por LT 'syreal' Jones para picoCTF 2023, consiste en interactuar con una terminal modificada que intenta corregir automáticamente los comandos introducidos por el usuario.

La dificultad principal es que la terminal modifica las palabras introducidas antes de ejecutarlas. Por ejemplo, un comando normal como `ls` puede ser transformado en `Is`, provocando que el sistema intente ejecutar un comando inexistente.

El objetivo es encontrar una forma de evadir este mecanismo de corrección para poder ejecutar comandos de Linux y finalmente obtener el contenido de `flag.txt`.

## 2. Conexión al servidor

Primero se realiza una conexión mediante SSH utilizando los datos proporcionados por el reto:

```bash
ssh -p 37114 ctf-player@chatelaine.cylabacademy.net
```

La contraseña proporcionada es:

```text
13792798
```

Después de iniciar sesión aparece el indicador:

```text
Special$
```

Esto indica que estamos dentro de la interfaz especial del reto.

## 3. Análisis del funcionamiento

Se comenzó probando comandos básicos de Linux.

Por ejemplo:

```bash
ls
```

La terminal modifica el comando antes de ejecutarlo. Esto impide utilizar directamente los comandos habituales.

El objetivo fue entonces encontrar una sintaxis válida de Bash que permitiera ejecutar comandos sin que fueran modificados de la manera esperada.

## 4. Bypass mediante comillas

Después de experimentar con la sintaxis de Bash, se encontró que era posible ejecutar comandos utilizando cuatro comillas dobles antes del comando:

```bash
""""ls
```

El resultado fue:

```text
blargh
```

Esto confirmó que se había conseguido ejecutar `ls` correctamente y que existía un directorio llamado `blargh`.

Este método funciona porque la interfaz de `Special` realiza modificaciones sobre el texto antes de que Bash interprete completamente la entrada. Las construcciones especiales de Bash pueden aprovechar esta diferencia entre el procesamiento del programa y la interpretación posterior del shell.

## 5. Enumeración del directorio

El siguiente paso fue comprobar el contenido de `blargh`.

Se intentó:

```bash
""""ls blargh
```

Sin embargo, en la instancia utilizada el corrector modificó `blargh` a `large`, produciendo:

```text
ls: cannot access 'large': No such file or directory
```

Esto demostró que el corrector también modifica algunos argumentos de los comandos.

Para este reto existen diferentes formas de evitar este problema. Una alternativa documentada consiste en utilizar expansión de parámetros de Bash:

```bash
${parameter=ls blargh}
```

Esta sintaxis permite que Bash ejecute posteriormente el comando `ls blargh`, mientras que el texto inicial de la entrada no comienza directamente con el comando que el corrector intenta modificar.

Al ejecutar correctamente la enumeración se obtiene:

```text
flag.txt
```

Por lo tanto, se determina que la ubicación del archivo es:

```text
blargh/flag.txt
```

## 6. Lectura de la flag

Una vez conocida la ubicación del archivo, se utiliza nuevamente la expansión de parámetros para ejecutar `cat`:

```bash
${parameter=cat blargh/flag.txt}
```

Otra forma documentada específicamente para este reto consiste en utilizar:

```bash
""""cat blargh/flag.txt
```

La segunda forma aprovecha el mismo bypass mediante las cuatro comillas utilizado anteriormente.

Al ejecutarlo, el servidor muestra el contenido de `flag.txt`.
## Notas adicionales

## Referencias