## Descripcion
Why search for the flag when I can make a bookmarklet to print it for me? Browse [here](http://xebec.cylabacademy.net:42393/), and find the flag!
## Solucion
## 1. Abrir el reto

Abre en el navegador:

[Página del reto Bookmarklet](http://xebec.cylabacademy.net:42393/?utm_source=chatgpt.com)

La página muestra un código JavaScript que comienza aproximadamente así:

```
javascript:(function() {
    var encryptedFlag = "...";
    var key = "picoctf";
    var decryptedFlag = "";

    for (var i = 0; i < encryptedFlag.length; i++) {
        decryptedFlag += String.fromCharCode(
            (encryptedFlag.charCodeAt(i) -
             key.charCodeAt(i % key.length) + 256) % 256
        );
    }

    alert(decryptedFlag);
})();
```

La función ya contiene **todo lo necesario para obtener la flag**. El código toma `encryptedFlag`, utiliza `picoctf` como clave y va recuperando cada carácter de la bandera.

---

## 2. Abrir la consola del navegador

En Chrome/Chromium presiona:

```
Ctrl + Shift + J
```

También puedes abrir las herramientas con:

```
F12
```

y seleccionar la pestaña:

```
Console
```

---

## 3. Copiar el JavaScript

Copia **el código completo que aparece en la página**, incluyendo:

```
javascript:(function() {
```

y hasta:

```
})();
```

No necesitas modificar el algoritmo.

Pégalo directamente en la consola y presiona **Enter**.

> Si Chrome muestra una advertencia sobre pegar código en la consola, escribe manualmente `allow pasting` cuando el navegador lo solicite y vuelve a pegar el código.
## Notas adicionales

## Referencias