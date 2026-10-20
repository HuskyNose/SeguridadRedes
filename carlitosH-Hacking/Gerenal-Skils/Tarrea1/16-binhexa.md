## Descripcion
How well can you perfom basic binary operations? Start searching for the flag here `nc xebec.cylabacademy.net 31557`
## Solucion
## 1. Descripción

El reto **Binhexa**, perteneciente a la categoría _General Skills_ de picoCTF 2024, consiste en realizar diferentes operaciones básicas utilizando números binarios.

El servidor proporciona dos números binarios y solicita realizar seis operaciones diferentes. Después de completar todas las operaciones, se debe proporcionar el resultado de la última operación convertido a hexadecimal.

## 2. Conexión al servidor

Para iniciar el reto se utiliza `netcat` con el siguiente comando:

```bash
nc xebec.cylabacademy.net 31557
```

El servidor proporcionó los siguientes números:

```text
Binary Number 1: 00101010
Binary Number 2: 01111000
```

A partir de estos valores se realizaron las seis operaciones solicitadas.

## 3. Pregunta 1 — Desplazamiento a la izquierda

La primera operación solicitada fue:

```text
Operation 1: '<<'
Perform a left shift of Binary Number 1 by 1 bits.
```

Se tomó el primer número:

```text
00101010
```

y se desplazó un bit hacia la izquierda:

```text
00101010 << 1
```

El resultado fue:

```text
01010100
```

Por lo tanto, se introdujo:

```text
01010100
```

## 4. Pregunta 2 — Suma binaria

La segunda operación fue una suma entre ambos números:

```text
00101010 + 01111000
```

Realizando la suma:

```text
  00101010
+ 01111000
----------
  10100010
```

El resultado fue:

```text
10100010
```

Por lo tanto, se introdujo:

```text
10100010
```

## 5. Pregunta 3 — Desplazamiento a la derecha

La tercera operación solicitó desplazar el segundo número un bit hacia la derecha:

```text
01111000 >> 1
```

El desplazamiento produce:

```text
01111000
→ 00111100
```

Por lo tanto, se introdujo:

```text
00111100
```

## 6. Pregunta 4 — Operación OR

La cuarta operación fue un OR (`|`) entre ambos números.

En una operación OR, el resultado de cada posición es `1` cuando al menos uno de los dos bits es `1`.

```text
  00101010
| 01111000
----------
  01111010
```

El resultado fue:

```text
01111010
```

Por lo tanto, se introdujo:

```text
01111010
```

## 7. Pregunta 5 — Operación AND

La quinta operación fue un AND (`&`) entre ambos números.

En una operación AND, el resultado solamente es `1` cuando ambos bits son `1`.

```text
  00101010
& 01111000
----------
  00101000
```

El resultado fue:

```text
00101000
```

Por lo tanto, se introdujo:

```text
00101000
```

## 8. Pregunta 6 — Multiplicación

La sexta y última operación fue una multiplicación:

```text
00101010 * 01111000
```

Primero se convirtieron los números binarios a decimal:

```text
00101010 = 42
01111000 = 120
```

Después se realizó la multiplicación:

```text
42 × 120 = 5040
```

Finalmente, el número decimal `5040` se convirtió nuevamente a binario:

```text
5040 = 1001110110000
```

Por lo tanto, el resultado binario de la sexta operación fue:

```text
1001110110000
```

## 9. Conversión del resultado a hexadecimal

El servidor solicitó:

```text
Enter the results of the last operation in hexadecimal:
```

Para convertir el resultado binario a hexadecimal se agregaron ceros a la izquierda hasta completar grupos de cuatro bits:

```text
1001110110000
```

se convierte en:

```text
0001 0011 1011 0000
```

Cada grupo corresponde a un dígito hexadecimal:

```text
0001 = 1
0011 = 3
1011 = B
0000 = 0
```

Por lo tanto:

```text
1001110110000₂ = 13B0₁₆
```

Se introdujo como respuesta final:

```text
13B0
```

## Notas adicionales

## Referencias
