## Descripcion
Find the flag being held on this server to get ahead of the competition

http://wily-courier.picoctf.net:60907/
## Solucion
No solo hay GET o POST, es HEAD
en la terminal usamos un:
```
┌──(kali㉿kali)-[~]
└─$ curl -s -I http://wily-courier.picoctf.net:60907/index.php
HTTP/1.1 200 OK
Date: Mon, 07 Sep 2026 16:23:12 GMT
Server: Apache/2.4.38 (Debian)
X-Powered-By: PHP/7.2.34
flag: picoCTF{r3j3ct_th3_du4l1ty_8b13f07}
Content-Type: text/html; charset=UTF-8

```

## Solucion 2
Ejecutar el siguiente script de python
```
import requests

url = "http://wily-courier.picoctf.net:60907/index.php"

# requests.head() equivale al parámetro -I de curl
respuesta = requests.head(url)

# Imprimimos la línea de estado (ej. HTTP/1.1 200 OK)
print(f"HTTP/1.1 {respuesta.status_code} {respuesta.reason}")

# Imprimimos los encabezados con el mismo formato de curl
for clave, valor in respuesta.headers.items():
    print(f"{clave}: {valor}")
```
## Notas adicionales

## Referencias
