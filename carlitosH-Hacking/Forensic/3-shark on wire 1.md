## Descripcion
We found this [packet capture](https://challenge-files.cylabacademy.net/library/e64f2c2aaf9bf531af7be1787c1407c47a4cc7b57f251d5108a1151e9721a2d6/shark-on-wire-1-capture.pcap). Recover the flag.
## Solucion
### 1. Descripción del reto

El reto **Shark on Wire 1** pertenece a la categoría **Forensics** y consiste en analizar una captura de tráfico de red para recuperar una bandera.

El archivo proporcionado por el reto es:

```
shark-on-wire-1-capture.pcap
```

Las pistas proporcionadas son:

> **Try using a tool like Wireshark**

> **What are streams?**

Estas pistas indican que debemos utilizar **Wireshark** y analizar los diferentes **streams** de la captura.

---

### 2. Descargar el archivo

Primero se descarga el archivo proporcionado por el reto.

Después comprobamos que se encuentre en nuestro directorio:

```
ls
```

---

### 3. Identificar el archivo

Utilizamos `file` para comprobar el tipo de archivo:

```
file shark-on-wire-1-capture.pcap
```

El resultado debe indicar que se trata de una captura de paquetes de red.

Por ejemplo:

```
PCAP capture file
```

El formato `.pcap` puede ser analizado utilizando herramientas como **Wireshark**.

---

### 4. Abrir la captura con Wireshark

Ejecutamos:

```
wireshark shark-on-wire-1-capture.pcap
```

También podemos abrir el archivo directamente desde la interfaz gráfica de Wireshark.

Una vez abierta la captura, podemos observar diferentes protocolos y paquetes de red.

---

### 5. Filtrar el tráfico UDP

Debido a que el reto hace referencia a los **streams**, primero podemos buscar tráfico UDP.

En la barra de filtros de Wireshark escribimos:

```
udp
```

y presionamos **Enter**.

Esto permite mostrar únicamente los paquetes que utilizan el protocolo UDP.

---

### 6. Seguir un UDP Stream

Seleccionamos uno de los paquetes UDP.

Después hacemos:

**Clic derecho → Follow → UDP Stream**

Esto abre una ventana donde podemos observar todos los datos que pertenecen a ese flujo de comunicación.

Al revisar los primeros streams podemos encontrar información que parece aleatoria o que no corresponde a la bandera.

Por lo tanto, debemos revisar los diferentes streams.

---

### 7. Revisar los diferentes streams

Dentro de la ventana **Follow UDP Stream**, Wireshark permite cambiar entre diferentes streams mediante el número de stream.

También podemos utilizar directamente el filtro:

```
udp.stream eq 0
```

Después:

```
udp.stream eq 1
```

y continuar:

```
udp.stream eq 2
```

```
udp.stream eq 3
```

```
udp.stream eq 4
```

```
udp.stream eq 5
```

```
udp.stream eq 6
```

En la captura original del reto, el **stream 6** contiene la bandera, mientras que existen otros streams que pueden contener información irrelevante o incluso una bandera falsa.

---

### 8. Encontrar la bandera

Podemos seleccionar directamente el sexto stream utilizando:

```
udp.stream eq 6
```

Después hacemos:

**Clic derecho sobre un paquete → Follow → UDP Stream**

El contenido del stream permite reconstruir la información enviada mediante los paquetes UDP.
## Notas adicionales

## Referencias
