## Descripcion
Can you break into this super secure portal?

[http://fickle-tempest.picoctf.net:65022](http://fickle-tempest.picoctf.net:65022/)
## Solucion
Inspeccionamos la pagina con CTRL + U, al inspeccionar veremos varios bloques desordenados: 
```
|   |
|---|
|if (checkpass.substring(0, split) == 'pico') {|
|if (checkpass.substring(split*6, split*7) == 'eb02') {|
|if (checkpass.substring(split, split*2) == 'CTF{') {|
|if (checkpass.substring(split*4, split*5) == 'ts_p') {|
|if (checkpass.substring(split*3, split*4) == 'lien') {|
|if (checkpass.substring(split*5, split*6) == 'lz_2') {|
|if (checkpass.substring(split*2, split*3) == 'no_c') {|
|if (checkpass.substring(split*7, split*8) == 'b45}') {|
|alert("Password Verified")|
```
Estan desordenados y ahi esta la bandera, para obtener la bandera tenemos que ordenar, para esto nos guiamos del "split"
## Notas adicionales

## Referencias
