
## Descripcion
If you want to hash with the best, beat this test!
## Solucion
# HashingJobApp

**Categoría:** General Skills – Easy  
**Plataforma:** picoMini 2022  
**Autor:** LT 'syreal' Jones

## 1. Descripción del reto

El reto consiste en conectarse a un servicio remoto mediante `netcat`. El servidor proporciona diferentes textos y solicita calcular su hash **MD5**.

El objetivo es calcular correctamente cada hash y enviarlo al servidor hasta completar el reto y obtener la bandera.

## 2. Conexión al servidor

Primero se estableció una conexión con el servidor utilizando el siguiente comando:

```bash
nc chatelaine.cylabacademy.net 33391
```

El comando `nc` permite establecer una conexión con el servicio remoto utilizando el puerto `33391`.

## 3. Obtener el texto

Después de conectarnos, el servidor mostró una instrucción similar a:

```text
Please md5 hash the text between quotes, excluding the quotes:
'Michelangelo'
```

El texto que se debe utilizar es únicamente el contenido que se encuentra entre las comillas.

Por ejemplo:

```text
Michelangelo
```

Las comillas no forman parte del texto que se debe procesar.

## 4. Calcular el hash MD5

Para calcular el hash se utilizó el comando:

```bash
echo -n "Michelangelo" | md5sum
```

y repetir las veces que sea necesario
## 9. Conclusión

En este reto se pra
## Notas adicionales

## Referencias