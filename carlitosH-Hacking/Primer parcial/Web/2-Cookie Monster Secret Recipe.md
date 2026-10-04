## Descripcion
##   
Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe? You can access the Cookie Monster [here](http://xebec.cylabacademy.net:40031/) and good luck
## Solucion
## 1. Abrir la página

Entra al reto:

[Cookie Monster Secret Recipe](http://xebec.cylabacademy.net:40031/?utm_source=chatgpt.com)

Te aparecerá una página de inicio de sesión.

## 2. Introducir cualquier usuario y contraseña

No necesitas conocer las credenciales reales.

Por ejemplo:

```
Usuario: test
Contraseña: test
```

Pulsa **Login**.

La página debería rechazar el acceso y mostrar un mensaje relacionado con revisar las cookies. Esto es precisamente la pista del reto.

## 3. Abrir las herramientas de desarrollador

En Chrome/Chromium:

```
Ctrl + Shift + I
```

Después entra en:

```
Application
   ↓
Storage
   ↓
Cookies
   ↓
http://xebec.cylabacademy.net:40031
```

También puedes hacerlo desde:

```
F12 → Application → Cookies
```

## 4. Buscar `secret_recipe`

En la lista de cookies encontrarás una llamada:

```
secret_recipe
```

Su valor será una cadena parecida a:

```
cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzXzZFODFGQzFFfQ==
```

**No copies necesariamente ese valor**, porque el valor puede cambiar en tu instancia de CylabAcademy. Debes utilizar el que aparece en tu navegador.

## 5. Identificar Base64

El valor tiene características típicas de **Base64**:

```
cGljb0NURnt...
```

y termina en:

```
==
```

Por lo tanto, podemos intentar decodificarlo.

Una forma sencilla es utilizar Python:

```
echo 'TU_COOKIE' | base64 -d
```

Por ejemplo:

```
echo 'cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzXzZFODFGQzFFfQ==' | base64 -d
```
## Notas adicionales

## Referencias