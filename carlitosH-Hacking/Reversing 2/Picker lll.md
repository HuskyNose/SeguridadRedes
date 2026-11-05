
## Descripcion
Can you figure out how this program works to get the flag? Connect to the program with netcat:

`$ nc xebec.cylabacademy.net 32345`

The program's source code can be downloaded [here](https://challenge-files.cylabacademy.net/library/a577115047ce25baf35085dc38de4247a8e18534b9f7f04f2459ab421183c437/picker-III.py).
## Solucion
El programa define una tabla con cuatro funciones, la función `win()` sigue existiendo en el programa, pero no está incluida en la tabla.
Hay tres funciones importantes
A. `write_variable()`
B. `filter_var_name()` y
C. `filter_value()`

La vulnerabilidad está en que `write_variable()` permite modificar `func_table`, pero el programa solamente comprueba que su longitud sea de 128 caracteres.

```
def check_table():
    global func_table

    if(len(func_table) != FUNC_TABLE_ENTRY_SIZE * FUNC_TABLE_SIZE):
        return False

    return True
```

```
FUNC_TABLE_SIZE = 4
FUNC_TABLE_ENTRY_SIZE = 32
```

4x34=128

El programa no verifica que los nombres de las funciones sean los originales. Solamente verifica la longitud.

```
table = " " * 96 + "win" + " " * 29
```

Este es el valor que modificara la tabla
```
print(len(table))
```

ya solo para asignarla a wrute_variable()
```
'                                ...'
```

enviamos una cadena, la cadena se evalúa como un valor de texto y no contiene ninguno de los caracteres prohibidos por `filter_value()` (`;`, `(` y `)`).
## Notas adicionales

## Referencias
