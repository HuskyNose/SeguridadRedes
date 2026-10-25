## Descripcion
We received an encrypted message. The modulus is built from primes large enough that factoring them isn’t an option, at least not today. See if you can make sense of the numbers and reveal the flag. Download the [message](https://challenge-files.cylabacademy.net/library/045cb85019ff34b1046bdea29511114f0f635e533109dc1b88bb3bc42b39658d/message.txt).
## Solucion
import re

  

# 1. Leer automáticamente n, e y c desde message.txt

with open("message.txt", "r") as f:

    content = f.read()

  

n = int(re.search(r"n\s*=\s*(\d+)", content).group(1))

e = int(re.search(r"e\s*=\s*(\d+)", content).group(1))

c = int(re.search(r"c\s*=\s*(\d+)", content).group(1))

  

# 2. Función de raíz n-ésima exacta sobre enteros (evita instalar gmpy2 en Windows)

def integer_nth_root(y, n_exp):

    low = 0

    high = 1 << ((y.bit_length() + n_exp - 1) // n_exp)

    while low <= high:

        mid = (low + high) // 2

        p = pow(mid, n_exp)

        if p == y:

            return mid, True

        elif p < y:

            low = mid + 1

        else:

            high = mid - 1

    return high, False

  

# 3. Calcular m = c^(1/e)

m, exact = integer_nth_root(c, e)

  

if exact:

    # 4. Convertir el entero m a bytes y decodificar en ASCII

    num_bytes = (m.bit_length() + 7) // 8

    flag = m.to_bytes(num_bytes, byteorder="big").decode("utf-8", errors="ignore")

    print(f"[+] Raíz exacta encontrada.")

    print(f"[+] Flag: {flag}")

else:

    print("[-] La raíz no es exacta; m^e sí superó el módulo n.")
## Notas adicionales

## Referencias
