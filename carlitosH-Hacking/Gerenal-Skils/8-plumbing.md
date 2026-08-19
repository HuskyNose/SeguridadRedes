
## Descripcion

Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?

Connect to fickle-tempest.picoctf.net 52015.
## Solucion
HuskyNose-academy@webshell:~$  nc fickle-tempest.picoctf.net 52015 | grep 
"picoCTF"
picoCTF{digital_plumb3r_11fffFE5}
## Notas adicionales
usamos para nc para conectarnos, pero solo nos va lanzar pura basura, asi que usamos un pipe y ponemos el comando grep
## Referencias