## Descripcion
A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher? Download the message [here](https://challenge-files.cylabacademy.net/library/0a2e91276318c0f6d400f5096fdaf87fcf57f37ebabf90004552502979a581c8/message.txt).
## Solucion
```
alfabeto = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"  
clave = "HRZUEVABDLIOJYTGNXCMWPKSQF"

mensaje = input("Introduce el mensaje cifrado: ")  
mensaje_descifrado = ""

for letra in mensaje:  
if letra.upper() in clave:  
posicion = clave.index(letra.upper())  
letra_original = alfabeto[posicion]

```
    if letra.islower():
        letra_original = letra_original.lower()

    mensaje_descifrado = mensaje_descifrado + letra_original
else:
    mensaje_descifrado = mensaje_descifrado + letra
```

print("\nMensaje descifrado:")  
print(mensaje_descifrado)
```
## Notas adicionales

## Referencias
Gemini Argon Alto, Sustitucion Monoalfabetica ejemplo:
![[Pasted image 20261024202136.png]]