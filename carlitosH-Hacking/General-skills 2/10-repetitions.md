## Descripcion
Can you make sense of this file?

Download the file [here](https://artifacts.picoctf.net/c/476/enc_flag).
## Solucion
solo usamos:
cat enc_flag | base64 -d | base64 -d | base64 -d
si sigue sacando texto basura solo repetimos base64 -d hasta que salga o usamos un script en python
## Notas adicionales

## Referencias
