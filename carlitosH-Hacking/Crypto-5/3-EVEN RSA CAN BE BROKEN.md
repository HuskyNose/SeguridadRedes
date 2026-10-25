## Descripcion
This service provides you an encrypted flag. Can you decrypt it with just N & e? Connect to the program with netcat:

`$ nc xebec.cylabacademy.net 32874`

The program's source code can be downloaded [here](https://challenge-files.cylabacademy.net/library/742b4d10be646510247831837d9876dafee7f7eb0eea7ee82eaf8f04981ef2d3/encrypt.py).
## Solucion
```
from Crypto.Util.number import long_to_bytes

print("EVEN RSA CAN BE BROKEN")
print()

N = int(input("Introduce N: "))
e = int(input("Introduce e: "))
c = int(input("Introduce el cyphertext: "))

# Comprobar si N es par
if N % 2 == 0:

    # Factorizar N
    p = 2
    q = N // 2

    print("\nFactores encontrados:")
    print("p =", p)
    print("q =", q)

    # Calcular la funcion totiente de Euler
    phi = (p - 1) * (q - 1)

    # Calcular la clave privada
    d = pow(e, -1, phi)

    # Descifrar el mensaje
    m = pow(c, d, N)

    # Convertir el resultado a texto
    flag = long_to_bytes(m)

    print("\nBandera recuperada:")
    print(flag.decode())

else:
    print("N es impar. Este ataque no se puede aplicar directamente.")
```
1. Se estableció una conexión con el servidor de Cylab Academy mediante Netcat para obtener los parámetros públicos de RSA y el texto cifrado.
    
2. Se observó que el módulo (N) era un número par, lo que permitió identificar inmediatamente uno de sus factores: (p=2).
    
3. Se calculó el segundo factor mediante (q=N/2).
    
4. Con ambos factores se obtuvo la función totiente de Euler, utilizando la expresión (\varphi(N)=(p-1)(q-1)).
    
5. Se calculó el exponente privado mediante el inverso modular de (e) respecto a (\varphi(N)).
    
6. Se descifró el mensaje mediante exponenciación modular y se convirtió el resultado numérico en bytes para recuperar el texto original.
## Notas adicionales
python -m pip install pycryptodome
## Referencias
`N % 2 == 0`Comprueba si el módulo es par.`p = 2`Establece el primer factor.`q = N // 2`Calcula el segundo factor.`phi = (p - 1) * (q - 1)`Calcula la función totiente de Euler.`pow(e, -1, phi)`Obtiene el exponente privado mediante el inverso modular.`pow(c, d, N)`Descifra el mensaje mediante exponenciación modular.`long_to_bytes(m)`Convierte el resultado entero en bytes.`flag.decode()`Interpreta los bytes como texto.