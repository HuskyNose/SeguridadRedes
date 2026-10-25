## Descripcion
Can you decrypt this message? Decrypt this [message](https://challenge-files.cylabacademy.net/library/848831bc0df5e68fe8f320c91c47f635bce35a7c8236c696f9478bfaf39cfd10/cipher.txt) using this key "CYLAB".
## Solucion
```
alfabeto = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

mensaje = input("Introduce el mensaje cifrado: ")  
clave = input("Introduce la clave: ")

mensaje = mensaje.upper()  
clave = clave.upper()

mensaje_descifrado = ""  
posicion_clave = 0

for letra in mensaje:  
if letra in alfabeto:  
posicion_mensaje = alfabeto.index(letra)  
posicion = posicion_clave % len(clave)  
letra_clave = clave[posicion]  
valor_clave = alfabeto.index(letra_clave)

```
    valor_original = (posicion_mensaje - valor_clave) % 26
    letra_original = alfabeto[valor_original]

    mensaje_descifrado = mensaje_descifrado + letra_original
    posicion_clave = posicion_clave + 1
else:
    mensaje_descifrado = mensaje_descifrado + letra
```

print("\nMensaje descifrado:")  
print(mensaje_descifrado)
```
## Notas adicionales

## Referencias
[https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher)