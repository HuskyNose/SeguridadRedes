## Descripcion

Can you find the flag in [file](https://challenge-files.picoctf.net/c_fickle_tempest/fd00e7cc9b263f22c323572d2d5fc37d170f8e58e99a91f8991d0f07c69b21ff/strings) without running it?
## Solucion

usamos el siguiente comando
```
strings strings | grep "picoCTF"
```
## Notas adicionales

strings: Escanea cualquier archivo y extrae _únicamente_ las secuencias de caracteres que son legibles para un humano ignorando todo el código máquina basura
## Referencias