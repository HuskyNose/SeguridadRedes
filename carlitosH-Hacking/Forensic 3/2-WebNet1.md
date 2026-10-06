## Descripcion
We found this [packet capture](https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/webnet1-capture.pcap) and [key](https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/picopico.key). Recover the flag.
## Solucion
### 1. Descarga los dos archivos

En Kali:

```
wget "https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/webnet1-capture.pcap" -O webnet1-capture.pcap

wget "https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/picopico.key" -O picopico.key
```

Comprueba que estén:

```
ls -l webnet1-capture.pcap picopico.key
```

### 2. Abre el `.pcap` con Wireshark

```
wireshark webnet1-capture.pcap
```

Ve a:

**Edit → Preferences → Protocols → TLS**

Busca **RSA Keys List** y agrega:

```
IP:       172.31.22.220
Port:     443
Protocol: http
Key File: picopico.key
```

La configuración de la clave RSA es precisamente lo que permite que Wireshark descifre el tráfico TLS capturado.

Después acepta y **recarga/reabre el `.pcap`**.

---

### 3. Busca el tráfico HTTP descifrado

En el filtro de Wireshark puedes utilizar:

```
http
```

Deberían aparecer paquetes HTTP que antes estaban ocultos dentro de TLS.

También puedes buscar directamente:

```
http contains "academy"
```

Al seguir uno de los streams encontrarás algo parecido a:

```
academy-Flag: academy{this.is.not.your.flag.anymore}
```

Es un señuelo colocado intencionalmente por el reto.

---

### 4. Busca el JPEG

En el tráfico HTTP aparece un archivo llamado:

```
vulture.jpg
```

Puedes extraerlo desde Wireshark mediante:

**File → Export Objects → HTTP**

Guárdalo, por ejemplo, en una carpeta llamada `out`.

Después:

```
ls out
```

Deberías encontrar:

```
vulture.jpg
```

---

### 5. Busca la bandera dentro del JPEG

Ejecuta:

```
strings out/vulture.jpg | grep pico
```

La salida contiene:

```
academy{honey.roasted.peanuts}
```
## Notas adicionales

## Referencias