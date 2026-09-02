## Descripcion
Can you break into this super secure portal?

[http://fickle-tempest.picoctf.net:64732](http://fickle-tempest.picoctf.net:64732/)
## Solucion
- **Inspecciona el desastre:** Abre el código fuente de la página (`Ctrl + U` en el navegador o ejecuta tu `curl`). Notarás que el script ahora es un bloque de texto horrendo, lleno de variables como `_0x5a46` y texto codificado.
    
- **Identifica la bóveda de datos:** La debilidad de la ofuscación en JavaScript es que, por más revuelta que esté la lógica, las cadenas de texto originales tienen que cargarse en memoria. Justo al inicio del script verás un arreglo (una lista entre corchetes `[ ]`) que contiene todas las palabras que usa el programa.
    
- **El Rompecabezas 2.0:** Si lees los elementos dentro de ese arreglo, ignorando la basura como `'getElementById'` o `'Password Verified'`, verás los fragmentos exactos de tu objetivo. No necesitas ejecutar el código ni desenredar la lógica de la función; el desarrollador simplemente cortó la bandera en pedazos y los guardó en esa lista.

## Solucion 2 
**1. El botón "Pretty Print" (El camino visual)** Los navegadores tienen un desofuscador básico integrado que formatea el código en un milisegundo.

- Abre las Herramientas de Desarrollador (**F12**).
    
- Ve a la pestaña **Sources** (Fuentes) y abre el código HTML del reto.
    
- En la esquina inferior izquierda del panel de código, verás un botón con dos llaves: **`{ }`**.
    
- Al darle clic, el navegador tomará esa línea gigante y la separará en una estructura perfectamente indentada y legible.
    

**2. Interrogar la Memoria (El camino de la Consola)** Dado que el navegador _tiene_ que cargar y procesar ese arreglo para que la página funcione, las piezas ya están flotando limpias en la memoria RAM de tu pestaña.

- Abre la pestaña **Console** (Consola) en tus herramientas de desarrollador.
    
- Escribe directamente el nombre de la variable del arreglo: **`_0x5a46`**
    
- Presiona **Enter**.
    
- La consola te escupirá la lista exacta, limpia y separada por índices `[0, 1, 2, 3...]`.
    

De esta forma, en lugar de forzar la vista buscando entre comillas y código basura, extraes la información procesada directamente del motor de JavaScript en menos de 5 segundos.
## Notas adicionales

## Referencias
