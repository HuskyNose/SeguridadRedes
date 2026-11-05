
## Descripcion
## Picker IV

Binary ExploitationMedium

by LT 'syreal' Jones

Can you figure out how this program works to get the flag? Connect to the program with netcat:

`$ nc chatelaine.cylabacademy.net 34942`

The program's source code can be downloaded [here](https://challenge-files.cylabacademy.net/library/29304f03408a71abe2959b78d93cf0ad4b599550b0dfc4ee3211c8376731d344/picker-IV.c). The binary can be downloaded [here](https://challenge-files.cylabacademy.net/library/29304f03408a71abe2959b78d93cf0ad4b599550b0dfc4ee3211c8376731d344/picker-IV).
## Solucion
Solicita una dirección hexadecimal.
Guarda la dirección introducida en `val`.
Convierte esa dirección en un puntero a función.
 Ejecuta la dirección mediante `foo()`.

objdump -d -M intel picker-IV | grep win

comando para encontrar la direccion win 
## Notas adicionales

## Referencias
