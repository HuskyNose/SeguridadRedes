
## Descripcion
Someone's commits seems to be preventing the program from working. Who is it?

You can download the challenge files here:

- [challenge.zip](https://challenge-files.cylabacademy.net/library/31eae587db829288524ad2f1581ec980aca2ad5f7e66908a5178390d1407cec5/challenge.zip)
## Solucion
**Open Git Bash here**

También puedes hacerlo desde Git Bash:

```
cd ~/Downloads/drop-in
```

Comprueba los archivos:

```
ls -la
```

Deberías ver algo parecido a:

```
.git
message.py
```

---

Revisar el archivo actual

Ejecuta:

```
cat message.py
```

Probablemente encontrarás algo parecido a:

```
print("Hello, World!"
```

El problema es que falta un paréntesis `)`.

Sin embargo, **no necesitamos arreglar el programa**. El objetivo es descubrir quién hizo el commit que lo dejó así.

---

 Revisar el historial del archivo

Aquí está la parte importante del reto.

Ejecuta:

```
git log -- message.py
```

## Notas adicionales

## Referencias