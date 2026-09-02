## Descripcion
Can you find the robots?

[http://fickle-tempest.picoctf.net:52635](http://fickle-tempest.picoctf.net:52635/)
## Solucion
- **Paso 1:** Abre el enlace del reto (`[http://fickle-tempest.picoctf.net:52635](http://fickle-tempest.picoctf.net:52635)`) en una pestaña de tu navegador web.
    
- **Paso 2:** Modifica la URL en la barra de direcciones agregando `/robots.txt` al final (quedando exactamente así: `[http://fickle-tempest.picoctf.net:52635/robots.txt](http://fickle-tempest.picoctf.net:52635/robots.txt)`) y presiona Enter.
    
- **Paso 3:** Inspecciona el texto plano que aparece en pantalla. Busca la línea que dice `Disallow:`. Esa línea te indicará la ruta del archivo o directorio que el creador intentó ocultar (por ejemplo, algo como `/directorio_secreto.html`).
    
- **Paso 4:** Vuelve a la barra de direcciones, borra `robots.txt` y escribe la ruta secreta que acabas de descubrir. Al entrar ahí, encontrarás tu bandera.
## Solucion 2
**Fase 1: El Reconocimiento** Lanza este comando para extraer el archivo de exclusión de robots en texto plano: `curl [http://fickle-tempest.picoctf.net:52635/robots.txt](http://fickle-tempest.picoctf.net:52635/robots.txt)`

**Fase 2: La Extracción** La terminal te imprimirá un par de líneas. Identifica la ruta que aparece justo después de la instrucción `Disallow:`. Toma esa ruta exacta (incluyendo la diagonal `/`) y concaténala al final de tu próximo comando: `curl [http://fickle-tempest.picoctf.net:52635/RUTA_SECRETA_AQUI](http://fickle-tempest.picoctf.net:52635/RUTA_SECRETA_AQUI)`

## Notas adicionales
Cuando un sitio se sube a internet, los motores de búsqueda (como Google) envían bots automáticos ("crawlers") para indexar todo su contenido. Para evitar que estos bots indexen paneles de administración, bases de datos o carpetas privadas, los administradores colocan un archivo público en la raíz del servidor llamado `robots.txt`. Este archivo contiene reglas `Disallow` (No permitir).
## Referencias
