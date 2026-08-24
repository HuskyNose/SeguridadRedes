## Descripcion

Can you look at the data in this binary? The bash script might help!

[static](https://challenge-files.picoctf.net/c_wily_courier/b06384f5fdb3a6e3f0f254d1064d203e7df4bf7e9a5780a95622523367d82bc0/static), [ltdis.sh](https://challenge-files.picoctf.net/c_wily_courier/b06384f5fdb3a6e3f0f254d1064d203e7df4bf7e9a5780a95622523367d82bc0/ltdis.sh)
## Solucion
usamos `cat ltdis.sh`
para ver el interior del archivo, solo tiene comandos de linux,

Ahora que sabemos que el archivo contiene comandos de linux, en la terminal usamos
`chmod +x ltdis.sh` --> esto para darle permisos de ejecucion a ltdis.sh

Despues solo usamos: `./ltdis.sh static` para generar el .txt
ya solo usamos: `grep "picoCTF" static.ltdis.strings.txt` para encontrar la bandera
## Notas adicionales
- **A todos (rápido):** `chmod +x archivo`

- **Solo al dueño (usuario):** `chmod u+x archivo`

- **Al dueño, grupo y otros:** `chmod a+x archivo`

- **Usando números (octal):** `chmod 755 archivo`
## Referencias
