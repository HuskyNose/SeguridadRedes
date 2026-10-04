## Descripcion
### 1. Descargar los archivos

Desde Kali/Linux puedes usar los enlaces proporcionados con `wget`:

```
wget "https://challenge-files.cylabacademy.net/library/617105c28abc79cef2487b00e5d07503f2b87fd29687ee960e7abe3a30294c8b/ende.py"

wget "https://challenge-files.cylabacademy.net/library/617105c28abc79cef2487b00e5d07503f2b87fd29687ee960e7abe3a30294c8b/password.txt"

wget "https://challenge-files.cylabacademy.net/library/617105c28abc79cef2487b00e5d07503f2b87fd29687ee960e7abe3a30294c8b/flag.txt.en"
```

Comprobamos que los archivos estén presentes:

```
ls
```

Debemos tener:

```
ende.py
password.txt
flag.txt.en
```

### 2. Revisar el script

Primero podemos ejecutar el programa sin argumentos:

```
python3 ende.py
```

El programa muestra una ayuda similar a:

```
Usage: ende.py (-e/-d) [file]
```

Esto nos indica que el programa tiene dos modos principales:

- `-e` → cifrar.
- `-d` → descifrar.

También podemos consultar la ayuda:

```
python3 ende.py -h
```

### 3. Obtener la contraseña

El reto proporciona un archivo llamado `password.txt`, por lo que podemos visualizarlo con:

```
cat password.txt
```

El contenido mostrado corresponde a la contraseña necesaria para descifrar el archivo.

### 4. Identificar el archivo cifrado

El archivo:

```
flag.txt.en
```

contiene la bandera cifrada.

La extensión `.en` indica que se trata del archivo que debemos descifrar.

### 5. Descifrar la bandera

Utilizamos el modo `-d` del programa:

```
python3 ende.py -d flag.txt.en
```
Colocamos la contraseña que conseguimos anteriormente y ahi estara la bandera
## Solucion

## Notas adicionales

## Referencias
