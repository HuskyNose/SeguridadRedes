## Descripcion

Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses.

Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools!

You can download the challenge files here:
## Solucion
Se usa una busqueda binaria, en mi caso, arme un codigo de python para encontrar la bandera
```
inicio = 1
fin = 1000

while inicio <= fin:
    medio = (inicio + fin) // 2

    print("¿Es", medio, "?")

    respuesta = input("Escribe 'mayor', 'menor' o 'correcto': ")

    if respuesta == "correcto":
        print("¡Encontrado! El número es:", medio)
        break
    elif respuesta == "mayor":
        inicio = medio + 1
    elif respuesta == "menor":
        fin = medio - 1
    else:
        print("Respuesta no válida")
```
## Notas adicionales

## Referencias
