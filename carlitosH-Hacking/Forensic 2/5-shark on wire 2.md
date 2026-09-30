## Descripcion
We found this [packet capture](https://challenge-files.cylabacademy.net/library/f76620763560ca0683be36e0ed4648743f969ab4d852fda0d8fb4d3ae21a173d/shark-on-wire-2-capture.pcap). Recover the flag that was pilfered from the network.
## Solucion
## 2. Descarga del archivo

Primero se descargó el archivo proporcionado por el reto utilizando `wget`:

```
wget "https://challenge-files.cylabacademy.net/library/f76620763560ca0683be36e0ed4648743f969ab4d852fda0d8fb4d3ae21a173d/shark-on-wire-2-capture.pcap" -O capture.pcap
```

Después se verificó el tipo de archivo:

```
file capture.pcap
```

El archivo corresponde a una captura de tráfico de red que puede ser analizada con Wireshark.

---

## 3. Análisis con Wireshark

Se abrió la captura utilizando:

```
wireshark capture.pcap
```

Para localizar los paquetes relevantes se utilizó el siguiente filtro:

```
udp.dstport == 22
```

Este filtro permite mostrar los paquetes UDP cuyo puerto de destino es el **22**.

También se puede utilizar:

```
udp and udp.port == 22
```

Al revisar los paquetes se observó que los **puertos de origen UDP cambiaban constantemente**.

Por ejemplo:

```
5000
5112
5105
5099
5111
5067
5084
5070
5123
...
```

Esto indica que los puertos de origen podrían estar siendo utilizados para transportar información.

---

## 4. Identificación de la información oculta

Al analizar los valores de los puertos se observó que varios de ellos eran superiores a `5000`.

La diferencia entre el puerto de origen y `5000` produce valores ASCII.

Por ejemplo:

```
5112 - 5000 = 112
5105 - 5000 = 105
5099 - 5000 = 99
5111 - 5000 = 111
```

Los valores obtenidos corresponden a caracteres ASCII:

|Puerto|Operación|ASCII|Carácter|
|---|---|---|---|
|5112|5112 - 5000|112|p|
|5105|5105 - 5000|105|i|
|5099|5099 - 5000|99|c|
|5111|5111 - 5000|111|o|

Por lo tanto:

```
112 105 99 111
```

se convierte en:

```
pico
```

Esto confirma que los puertos de origen contienen caracteres codificados mediante ASCII.

---

## 5. Extracción automática con Python

Para evitar convertir manualmente todos los puertos, se utilizó Python junto con Scapy.

Primero se instaló Scapy:

```
sudo apt update
sudo apt install python3-scapy
```

Se verificó que funcionara correctamente:

```
python3 -c "from scapy.all import *; print('Scapy funcionando')"
```

Después se creó el archivo:

```
nano extract.py
```

Con el siguiente código:

```
from scapy.all import *

packets = rdpcap("capture.pcap")

flag = ""

for packet in packets:
    if UDP in packet and packet[UDP].dport == 22:
        if packet[UDP].sport > 5000:
            flag = flag + chr(packet[UDP].sport - 5000)

print(flag)
```

---

## 6. Funcionamiento del script

### Importar Scapy

```
from scapy.all import *
```

Permite utilizar las funciones necesarias para analizar paquetes de red.

### Leer la captura

```
packets = rdpcap("capture.pcap")
```

Carga todos los paquetes almacenados en `capture.pcap`.

### Crear la variable de la bandera

```
flag = ""
```

Se utiliza para ir almacenando los caracteres encontrados.

### Recorrer los paquetes

```
for packet in packets:
```

Analiza cada paquete de la captura.

### Buscar paquetes UDP con destino al puerto 22

```
if UDP in packet and packet[UDP].dport == 22:
```

Solo se procesan los paquetes que utilizan UDP y cuyo puerto de destino es `22`.

### Obtener los caracteres ocultos

```
if packet[UDP].sport > 5000:
    flag = flag + chr(packet[UDP].sport - 5000)
```

Se verifica que el puerto de origen sea mayor que `5000`.

Después:

1. Se resta `5000` al puerto.
2. El resultado se convierte a ASCII mediante `chr()`.
3. El carácter obtenido se agrega a `flag`.

Por ejemplo:

```
5112 - 5000 = 112
chr(112) = p
```

---

## 7. Ejecución

El script se ejecutó mediante:

```
python3 extract.py
```

El programa recorrió automáticamente los paquetes, extrajo los puertos de origen utilizados para ocultar la información y convirtió los valores a caracteres ASCII.

Como resultado se obtuvo:

```
academy{p1LLf3r3d_data_v1a_st3g0}
```

---

## 8. Resultado

La bandera obtenida del reto **Shark on Wire 2** fue:

```
academy{p1LLf3r3d_data_v1a_st3g0}
```
## Notas adicionales

## Referencias
