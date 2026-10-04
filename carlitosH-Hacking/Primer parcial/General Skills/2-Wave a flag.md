## Descripcion
Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...

[warm](https://challenge-files.picoctf.net/c_wily_courier/70013ed41d4cfe2bb48628471dac6fc12238b5dbe164301ae3b4e35277b1e80b/warm)
## Solucion
descargarmos el archivo, le damos permiso al archivo:
chmod +x warm
y ya solo usamos el comando que nos da en la pista
./warm -h
## Notas adicionales
**`-h` y `--help`?** Son un estándar universal en Linux y en el desarrollo de software. Cuando ejecutas un programa desconocido, si le pasas alguna de estas banderas, el programa detendrá su ejecución normal y, en su lugar, imprimirá en tu pantalla un manual de instrucciones sobre cómo utilizarlo
## Referencias