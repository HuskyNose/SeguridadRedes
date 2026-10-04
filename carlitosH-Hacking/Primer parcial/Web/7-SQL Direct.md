## Descripcion
Connect to this PostgreSQL server and find the flag! `psql -h xebec.cylabacademy.net -p 25219 -U postgres pico`

Password is `postgres`
## Solucion
# SQL Direct — Comandos utilizados

### 1. Conectarse al servidor PostgreSQL

```text
psql -h xebec.cylabacademy.net -p 25219 -U postgres pico
```

**Descripción:** Establece una conexión con el servidor PostgreSQL utilizando el usuario `postgres` y la base de datos `pico`.

Cuando se solicitó la contraseña, se introdujo:

```text
postgres
```

### 2. Mostrar las tablas disponibles

```text
\dt
```

**Descripción:** Muestra las tablas disponibles dentro de la base de datos actual. Entre ellas se encontró la tabla `flags`.

### 3. Consultar la estructura de la tabla

```text
\d flags
```

**Descripción:** Muestra la estructura de la tabla `flags`, incluyendo sus columnas y tipos de datos.

### 4. Obtener el contenido de la tabla

```text
SELECT * FROM flags;
```

**Descripción:** Consulta todos los registros almacenados en la tabla `flags`. En los resultados se encontró la bandera del reto.

### Resumen

```text
Conexión PostgreSQL → \dt → tabla flags → SELECT * FROM flags → Flag
```

**Resultado:** La bandera se encontraba almacenada directamente en la tabla `flags`.
## Notas adicionales

## Referencias
