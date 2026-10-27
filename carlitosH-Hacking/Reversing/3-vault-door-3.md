## Descripcion
This vault uses for-loops and byte arrays. The source code for this vault is here: [VaultDoor3.java](https://challenge-files.cylabacademy.net/library/64ed47ea66574a28e2f23bbe36be348987a9ff131641bf451b1c04bb7b3e2d9f/VaultDoor3.java)
## Solucion
Tabla de reconstruccion
(Del indice 0 al 7 es en orden, del 8 al 15 solo hay que invertir esos caracteres)

|**Índice (i)**|**Par / Impar**|**Carácter en buffer**|**¿De qué posición viene?**|**Carácter real en password[i]**|
|---|---|---|---|---|
|**16**|Par|`6`|`buffer[46 - 16]` = `buffer[30]`|**`4`**|
|**17**|Impar|`g`|Se queda igual (`buffer[17]`)|**`g`**|
|**18**|Par|`d`|`buffer[46 - 18]` = `buffer[28]`|**`r`**|
|**19**|Impar|`4`|Se queda igual (`buffer[19]`)|**`4`**|
|**20**|Par|`e`|`buffer[46 - 20]` = `buffer[26]`|**`m`**|
|**21**|Impar|`_`|Se queda igual (`buffer[21]`)|**`_`**|
|**22**|Par|`u`|`buffer[46 - 22]` = `buffer[24]`|**`4`**|
|**23**|Impar|`_`|Se queda igual (`buffer[23]`)|**`_`**|
|**24**|Par|`4`|`buffer[46 - 24]` = `buffer[22]`|**`u`**|
|**25**|Impar|`_`|Se queda igual (`buffer[25]`)|**`_`**|
|**26**|Par|`m`|`buffer[46 - 26]` = `buffer[20]`|**`e`**|
|**27**|Impar|`7`|Se queda igual (`buffer[27]`)|**`7`**|
|**28**|Par|`r`|`buffer[46 - 28]` = `buffer[18]`|**`d`**|
|**29**|Impar|`e`|Se queda igual (`buffer[29]`)|**`e`**|
|**30**|Par|`4`|`buffer[46 - 30]` = `buffer[16]`|**`6`**|
|**31**|Impar|`2`|Se queda igual (`buffer[31]`)|**`2`**|
## Notas adicionales

## Referencias