## Descripcion
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?
## Solucion
- **Identificación de la vulnerabilidad:** A partir del nombre del reto (SOAP) y el objetivo explícito de leer un archivo interno del servidor (`/etc/passwd`), determinaste que la aplicación era vulnerable a un ataque de Inyección de Entidades Externas XML (XXE).
    
- **Creación de la entidad maliciosa:** Construiste un bloque de código XML definiendo una variable externa personalizada mediante la etiqueta `<!ENTITY xxe SYSTEM "file:///etc/passwd">`. Esto instruía al motor XML a cargar el contenido de ese archivo del sistema operativo.
    
- **Infiltración en la estructura:** Inyectaste esa entidad (`&xxe;`) dentro de la etiqueta `<ID>` que el servidor esperaba recibir de forma legítima, asegurando que el contenido del archivo se reflejara en la respuesta.
    
- **Reconocimiento del endpoint (Troubleshooting):** Al lanzar el ataque inicial hacia la raíz del sitio (`/`), chocaste contra un error _405 Method Not Allowed_. Descubriste que la petición POST debía apuntar estrictamente a la ruta de procesamiento de datos: `/data`.
    
- **Ejecución del ataque (Inyección por terminal):** Disparaste la petición final utilizando `curl -X POST`, forzando la cabecera `Content-Type: application/xml` para que el servidor aceptara el formato, y enviando tu payload hacia el endpoint `/data`.
    
- **Extracción de la bandera:** El servidor parseó el XML de forma insegura, ejecutó la llamada al sistema para leer el archivo de contraseñas de Linux, y te devolvió su contenido completo (donde estaba escondida la bandera) directamente en la salida de tu terminal.
## Notas adicionales

## Referencias
