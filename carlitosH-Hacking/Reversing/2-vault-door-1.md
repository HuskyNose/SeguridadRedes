## Descripcion
This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: [VaultDoor1.java](https://challenge-files.cylabacademy.net/library/9009823ee26b4bc37609526fc19c7ab48e8967196dc49b7e7745416752b61b9b/VaultDoor1.java)
## Solucion
Entras al codigo, en la funcion checkPassword esta la contraseña pero desordenada y caracrter por carcter, se puede obtener si ordenas los caracteres manualmente o automatizarlo 
```
import re

archivo = open("VaultDoor1.java", "r", encoding="utf-8")  
codigo = archivo.read()  
archivo.close()

coincidencias = re.findall(  
r"password.charAt((\d+))\s*==\s*'([^']*)'",  
codigo  
)

clave = [""] * 32

for indice, caracter in coincidencias:  
clave[int(indice)] = caracter

if "" in clave:  
print("Faltan caracteres por encontrar.")  
else:  
contrasena = "".join(clave)

print("Contraseña reconstruida:")
print(contrasena)

print("\nBandera:")
print("academy{" + contrasena + "}")
```
## Notas adicionales

## Referencias