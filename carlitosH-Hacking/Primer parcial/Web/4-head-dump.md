## Descripcion
Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.

The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden. The website is running [picoCTF News](http://chatelaine.cylabacademy.net:39226/).
## Solucion
### 1. Abre la página del reto

Entra en:

```
http://chatelaine.cylabacademy.net:39226/
```

Verás la página **PicoCTF News**, con varios artículos.

---

### 2. Busca el artículo de API Documentation

En la página principal hay un enlace relacionado con:

```
API Documentation
```

Haz clic ahí.

Esto lleva a:

```
/api-docs
```

La página usa **Swagger UI**, donde se muestran los endpoints disponibles de la aplicación.

También puedes entrar directamente:

```
http://chatelaine.cylabacademy.net:39226/api-docs
```

---

### 3. Busca el endpoint `heapdump`

Dentro de Swagger encontrarás diferentes endpoints.

Busca:

```
GET /heapdump
```

Este es el endpoint importante porque genera un **heap dump**, es decir, un archivo que contiene información de la memoria del proceso del servidor.

En Swagger puedes abrirlo y ejecutar:

```
GET /heapdump
```

---

### 4. Descarga el archivo

Al ejecutar el endpoint se descargará un archivo con extensión:

```
.heapsnapshot
```

---

### 5. Busca la bandera desde la terminal

Esta es la forma más cómoda.

Primero entra a la carpeta donde descargaste el archivo:

```
cd ~/Downloads
```

Después puedes buscar directamente:

```
grep -a "academy{" *.heapsnapshot
```

La opción `-a` hace que `grep` trate el archivo como texto aunque contenga datos que normalmente identificaría como binarios.
## Notas adicionales

## Referencias
