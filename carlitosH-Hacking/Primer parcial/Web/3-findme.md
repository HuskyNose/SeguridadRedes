## Descripcion
Help us test the form by submiting the username as `test` and password as `test!` The website running [here](http://chatelaine.cylabacademy.net:31462/).
## Solucion
No pude solucionarlo usando burp e interceptando la peticion de la pagina, asi que use el siguiente codigo de python:
```

python3 - <<'PY'
import requests
import re
import base64
from urllib.parse import urljoin

url = "http://chatelaine.cylabacademy.net:40556/login"

s = requests.Session()

r = s.post(
    url,
    data={
        "username": "test",
        "password": "test!"
    },
    allow_redirects=False
)

print("\n[+] RESPUESTA DEL LOGIN")
print("Status:", r.status_code)
print("Location:", r.headers.get("Location"))

while r.is_redirect:
    location = r.headers.get("Location")

    if location:
        siguiente = urljoin(r.url, location)

        print("\n[+] REDIRECCION:")
        print(siguiente)

        partes = re.findall(r'[A-Za-z0-9+/]{16,}={0,2}', siguiente)

        for parte in partes:
            try:
                decodificado = base64.b64decode(parte).decode()
                print("[+] Base64:", parte)
                print("[+] Decodificado:", decodificado)
            except:
                pass

        r = s.get(siguiente, allow_redirects=False)

    else:
        break

    texto = r.text

    partes = re.findall(r'[A-Za-z0-9+/]{16,}={0,2}', texto)

    for parte in partes:
        try:
            decodificado = base64.b64decode(parte).decode()

            if "picoCTF" in decodificado or "the_way" in decodificado:
                print("\n[+] CADENA ENCONTRADA:")
                print(parte)
                print("[+] Decodificado:", decodificado)

        except:
            pass

print("\n[+] URL FINAL:", r.url)
PY
```
## Notas adicionales

## Referencias