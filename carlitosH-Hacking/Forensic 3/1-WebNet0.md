## Descripcion
We found this [packet capture](https://challenge-files.cylabacademy.net/library/2d15538465c5948f0f0626d0cdd271f74363c00aa99d694730fe98331946ab88/webnet0-capture.pcap) and [key](https://challenge-files.cylabacademy.net/library/2d15538465c5948f0f0626d0cdd271f74363c00aa99d694730fe98331946ab88/picopico.key). Recover the flag.
## Solucion
# WebNet0

## 1. Descripción del reto

El reto **WebNet0** pertenece a la categoría **ForensicsHard** de picoCTF 2019. Se proporciona una captura de tráfico de red (`webnet0-capture.pcap`) y una clave privada (`picopico.key`).

El objetivo es analizar la captura, descifrar el tráfico TLS y recuperar la bandera.

## 2. Archivos utilizados

Los archivos proporcionados por el reto fueron:

```text
webnet0-capture.pcap
picopico.key
```

Se colocaron ambos archivos en la misma carpeta para facilitar el análisis.

## 3. Abrir la captura

Se abrió el archivo `.pcap` utilizando Wireshark:

```bash
wireshark webnet0-capture.pcap
```

Wireshark permitió visualizar los paquetes capturados y analizar las comunicaciones realizadas durante la conexión.

## 4. Identificar el tráfico TLS

Al revisar los paquetes se observó que parte de la comunicación estaba protegida mediante **TLS**.

Esto impedía visualizar directamente el contenido de las peticiones y respuestas HTTP.

La pista del reto indica que es necesario utilizar la clave proporcionada para descifrar el tráfico.

## 5. Configurar la clave privada en Wireshark

Dentro de Wireshark se ingresó a:

```text
Edit → Preferences → Protocols → TLS
```

Después se agregó el archivo:

```text
picopico.key
```

en la configuración correspondiente a las claves RSA/TLS.

Finalmente se aplicaron los cambios.

## 6. Analizar el tráfico descifrado

Después de configurar la clave, se revisó nuevamente la captura.

Se utilizó el filtro:

```text
http
```

Esto permitió localizar las comunicaciones HTTP que podían ser analizadas después del descifrado.

## 7. Seguir el flujo de comunicación

Se seleccionó uno de los paquetes relacionados con la comunicación y se utilizó la opción:

```text
Follow → TLS Stream
```

Esto permitió reconstruir la comunicación entre el cliente y el servidor.

Al revisar los datos recuperados se buscó información relacionada con la bandera.

## 8. Recuperar la bandera

Dentro de la comunicación descifrada se encontró la bandera:

```text
picoCTF{nongshim.shrimp.crackers}
```

## 9. Resultado

La bandera obtenida fue:

```text
academy{nongshim.shrimp.crackers}
```

## 10. Conclusión

El reto se resolvió mediante el análisis de una captura de tráfico de red utilizando Wireshark. Debido a que la comunicación estaba protegida mediante TLS, fue necesario utilizar el archivo `picopico.key` proporcionado por el reto para poder analizar el contenido de la comunicación.

Después de descifrar el tráfico y seguir el flujo correspondiente, fue posible localizar y recuperar la bandera.
## Notas adicionales

## Referencias

