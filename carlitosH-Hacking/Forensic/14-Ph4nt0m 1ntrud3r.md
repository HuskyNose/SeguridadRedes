## Descripcion
A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag.

To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder!

Find the PCAP file here [Network Traffic PCAP file](https://challenge-files.cylabacademy.net/library/88815ae7a4641c35f494d4d4b56e618428fe5cfb6a8b47c7a600eb98d670a72b/myNetworkTraffic.pcap) and try to get the flag.
## Solucion
### Paso 1. Descargar el archivo PCAP

Se descargó el archivo `myNetworkTraffic.pcap` desde el enlace proporcionado por la plataforma. Posteriormente, se verificó el tipo de archivo para confirmar que correspondiera a una captura de tráfico de red.

```bash
file myNetworkTraffic.pcap
```

### Paso 2. Analizar el tráfico con Wireshark

Se abrió la captura utilizando Wireshark para examinar los paquetes transmitidos, sus direcciones de origen y destino, los protocolos utilizados y las marcas de tiempo.

Se prestó especial atención a los paquetes que contenían datos, ya que podían incluir fragmentos de información ocultos.

### Paso 3. Filtrar los paquetes TCP

Se aplicó el siguiente filtro de visualización en Wireshark:

```text
tcp.len > 0
```

Este filtro permite mostrar los paquetes TCP que contienen datos en su segmento de carga útil, facilitando el análisis de la información transmitida.

### Paso 4. Extraer los datos mediante TShark

Se utilizó TShark para extraer el número de paquete, la marca de tiempo y el contenido hexadecimal de cada paquete que cumplía con el filtro.

```bash
tshark -r myNetworkTraffic.pcap -Y "tcp.len > 0" \
-T fields -e frame.number -e frame.time_epoch -e tcp.payload
```

El resultado mostró 22 paquetes con datos. Los valores de `tcp.payload` estaban representados en hexadecimal, por lo que fue necesario convertirlos para examinar su contenido.

### Paso 5. Convertir los datos hexadecimales

Se utilizó Python para convertir los valores hexadecimales a texto legible.

```python
datos = "657a46305833633063773d3d"
texto = bytes.fromhex(datos).decode("utf-8")
print(texto)
```

Este procedimiento permitió observar que los datos contenían cadenas con una estructura compatible con Base64.

### Paso 6. Analizar las marcas de tiempo

Se compararon las marcas de tiempo de los paquetes para determinar el orden temporal en que se transmitieron los fragmentos. Este análisis es importante porque el orden numérico de los paquetes no necesariamente coincide con el orden en que deben reconstruirse los datos ocultos.

### Paso 7. Decodificar la información

Se utilizó Base64 para decodificar los fragmentos identificados y analizar el texto resultante. Los fragmentos se examinaron individualmente antes de determinar cuáles debían combinarse para recuperar la bandera.
## Notas adicionales

## Referencias
