## Descripcion
There is some interesting information hidden around this site. Can you find it?

http://wily-courier.picoctf.net:52237/
## Solucion

**Tus Objetivos de Extracción:**

- **Parte 1 (Código Fuente HTML):** Ejecuta `curl -s [http://wily-courier.picoctf.net:52237/](http://wily-courier.picoctf.net:52237/) | grep "flag"` para filtrar el comentario oculto en la página principal.
    
- **Parte 2 (Hoja de Estilos):** Revisa los comentarios de diseño ejecutando `curl -s [http://wily-courier.picoctf.net:52237/mycss.css](http://wily-courier.picoctf.net:52237/mycss.css)`.
    
- **Parte 3 (Rutas Restringidas):** Como vimos en retos anteriores, los bots siempre revisan `robots.txt`. Ejecuta `curl -s [http://wily-courier.picoctf.net:52237/robots.txt](http://wily-courier.picoctf.net:52237/robots.txt)`.
    
- **Parte 4 (Configuración de Apache):** El archivo anterior te dará una pista sobre cómo el servidor web (Apache) maneja los accesos. Su archivo de configuración perimetral suele estar oculto. Ejecuta `curl -s [http://wily-courier.picoctf.net:52237/.htaccess](http://wily-courier.picoctf.net:52237/.htaccess)`.
    
- **Parte 5 (Metadatos de macOS):** La pista anterior menciona que el creador usa una Mac. macOS siempre deja un archivo invisible en sus carpetas para guardar preferencias de vista. Ejecuta `curl -s [http://wily-courier.picoctf.net:52237/.DS_Store](http://wily-courier.picoctf.net:52237/.DS_Store)`
## Notas adicionales

## Referencias