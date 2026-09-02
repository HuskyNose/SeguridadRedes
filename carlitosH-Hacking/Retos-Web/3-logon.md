## Descripcion
The factory is hiding things from all of its users.

Can you login as Joe and find what they've been looking at? [http://fickle-tempest.picoctf.net:50190](http://fickle-tempest.picoctf.net:50190/)
## Solucion
Hacemos un logeo normal con cualquier usuario y contraseña para crear las cookies
Ahora nos vamos al editor de cookies de la pagina, seleccionamos la cookie de admin, ahi editamos admin donde dice value de False a True

## Solucion 2
- **El Ataque por Terminal (`curl`):** Ya que tienes la consola abierta, puedes saltarte el formulario de inicio de sesión y disparar una petición directamente a la ruta protegida, inyectando la cookie falsificada en las cabeceras HTTP: `curl --cookie "admin=True" [http://fickle-tempest.picoctf.net:50190/flag](http://fickle-tempest.picoctf.net:50190/flag)`
    
- **El Ataque Gráfico (DevTools del Navegador):**
    
    1. Abre el enlace en tu navegador e inicia sesión con credenciales inventadas (ej. `a` / `a`).
        
    2. Una vez dentro, presiona **F12** para abrir las herramientas de desarrollador.
        
    3. Dirígete a la pestaña **Aplicación** (Chrome/Edge) o **Almacenamiento** (Firefox).
        
    4. En el panel lateral, despliega la sección de **Cookies** y selecciona la URL del reto.
        
    5. Verás una tabla con una variable llamada `admin` cuyo valor es `False`. Haz doble clic sobre el `False`, bórralo, escribe `True` y presiona Enter.
        
    6. Recarga la página con **F5**.
        

Al inyectar el parámetro `admin=True`, el backend leerá tu cookie, asumirá que eres un administrador legítimo y renderizará la bandera en la pantalla. ¡Ejecuta la modificación y cóbrate tu premio!
## Notas adicionales

## Referencias