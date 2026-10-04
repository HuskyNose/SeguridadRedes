## Descripcion
Play this short game to get familiar with terminal applications and some of the most important rules in scope for picoCTF.
## Solucion
##  Conexión al servidor

Primero se ejecutó el siguiente comando:

```
nc xebec.cylabacademy.net 34120
```

Este comando establece una conexión mediante **Netcat** con el servidor del reto utilizando el puerto `34120`.

##  Interacción con el juego

Una vez establecida la conexión, el programa comienza a mostrar una historia y diferentes instrucciones.

Cuando aparecía:

```
(Press Enter to continue...)
```

se presionó **Enter** para continuar.

##  Primera decisión

Durante el juego se presentó una pregunta con diferentes opciones. La opción correcta fue:

```
c
```

Esta opción permite continuar siguiendo las reglas establecidas por el reto.

##  Segunda decisión

Posteriormente se presentó otra selección de opciones. La respuesta correcta fue:

```
a
```

Con esta opción se continúa con el juego normalmente.

##  Finalización del juego

Después de seleccionar las opciones correctas, el programa continuó automáticamente con la ejecución del juego.

Se esperó a que terminara el proceso y se presionó **Enter** cuando fue solicitado.

Finalmente, el programa mostró un mensaje indicando que se había encontrado la bandera.


## Referencias
