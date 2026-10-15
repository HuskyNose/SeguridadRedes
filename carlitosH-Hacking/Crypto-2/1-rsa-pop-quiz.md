## Descripcion
## rsa-pop-quiz

CryptographyHard

by wparks/nmontierth·picoCTF 2019

Class, take your seats! It's PRIME-time for a quiz... `nc chatelaine.cylabacademy.net 22022`
## Solucion
### 1. Parámetros Básicos y Generación de Claves

El servidor comenzó evaluando la comprensión de los componentes fundamentales de RSA: los números primos y el módulo.

- **Cálculo del módulo ($n$):** Si se conocen los primos $p$ y $q$, obtener el módulo es una operación trivial.
    
    $$n = p \times q$$
    
- **Despeje de un factor ($q$):** Si el reto proporciona $n$ y uno de sus primos (por ejemplo, $p$), recuperar el primo faltante es factible y rápido mediante división entera.
    
    $$q = \frac{n}{p}$$
    
- **Función indicatriz de Euler ($\phi(n)$):** Teniendo ambos primos, se puede calcular la función totiente, la cual es el núcleo para derivar las claves.
    
    $$\phi(n) = (p-1) \times (q-1)$$
    

### 2. Viabilidad y la Seguridad de RSA

Varias preguntas del servidor actuaron como "trampas" para evaluar si se conoce qué operaciones son computacionalmente imposibles en criptografía asimétrica.

- **La factorización:** El servidor entregó únicamente una clave pública ($n$ y $e$) gigante y pidió los valores de $p$ y $q$. Se respondió que **NO** era factible (N). La seguridad de RSA radica precisamente en que factorizar un $n$ lo suficientemente grande es computacionalmente inviable.
    
- **Descifrado sin clave privada:** De igual forma, el servidor dio un texto cifrado ($c$) y el módulo ($n$), pidiendo el texto plano ($m$). Sin los factores primos para generar la clave privada, esto tampoco es factible, por lo que la respuesta correcta volvió a ser **N**.
    

### 3. Cifrado Matemático

- **Operación directa:** Se comprobó que cualquier usuario con la clave pública puede cifrar un mensaje. Dado un texto plano $m$, el proceso fue elevarlo al exponente público y aplicar el módulo.
    
    $$c = m^e \pmod n$$
    

### 4. Generación de la Clave Privada y el Ataque Final

La culminación del reto requirió realizar un descifrado completo aprovechando una mala configuración (la filtración de $p$). El servidor proporcionó el exponente $e$, el primo $p$, el módulo $n$ y el texto cifrado $c$.

El procedimiento documentado fue el siguiente:

1. **Obtener el factor faltante:** $q = \frac{n}{p}$
    
2. **Calcular el totiente:** $\phi(n) = (p-1) \times (q-1)$
    
3. **Derivar la clave privada ($d$):** Se calculó el inverso multiplicativo modular de $e$ módulo $\phi(n)$.
    
    $$d \equiv e^{-1} \pmod{\phi(n)}$$
    
4. **Descifrar el mensaje:**
    
    $$m = c^d \pmod n$$
    

El resultado numérico arrojado por esta operación fue:

`12398954807676569242017981049973013411282548937863661020322858792013936891919269469280821629`
## Notas adicionales
codigo para el ultimo problema:
```
# Valores proporcionados por el reto

e = 65537

p = 153143042272527868798412612417204434156935146874282990942386694020462861918068684561281763577034706600608387699148071015194725533394126069826857182428660427818277378724977554365910231524827258160904493774748749088477328204812171935987088715261127321911849092207070653272176072509933245978935455542420691737433

n = 23952937352643527451379227516428377705004894508566304313177880191662177061878993798938496818120987817049538365206671401938265663712351239785237507341311858383628932183083145614696585411921662992078376103990806989257289472590902167457302888198293135333083734504191910953238278860923153746261500759411620299864395158783509535039259714359526738924736952759753503357614939203434092075676169179112452620687731670534906069845965633455748606649062394293289967059348143206600765820021392608270528856238306849191113241355842396325210132358046616312901337987464473799040762271876389031455051640937681745409057246190498795697239

c = 12000545632287900492877619349317721637653160705411720471647731809273608657460264055860456124044106831566818170307028365265800012639372138798588783659629042349046809125733464074033358016595056525219593944624280233308312106323783751355866969666935164246947802991438562324370194556629193300661044217915509108958465648653744225292915001998809557948310636960866716122190479519488670733902137839521714018158362220855636907876667659428099048406691095036485318995829391666691280811282737135678251420397334365838648933020188135043959742261689501976232297530829749647472925867237932026077830046205627460745576072669709445288800

  

# 1. Calcular q

q = n // p

  

# 2. Calcular phi(n)

phi = (p - 1) * (q - 1)

  

# 3. Calcular la clave privada d (inverso modular de e mod phi)

# Nota: pow(a, -1, m) funciona en Python 3.8+

d = pow(e, -1, phi)

  

# 4. Desencriptar el mensaje m = c^d mod n

plaintext = pow(c, d, n)

  

print("El plaintext (número) a enviar es:")

print(plaintext)

  

# Opcional: Convertirlo a texto legible (ASCII/bytes) si el reto lo pide después

try:

    from Crypto.Util.number import long_to_bytes

    print("\nEl plaintext convertido a texto es:")

    print(long_to_bytes(plaintext).decode())

except ImportError:

    # Alternativa por si no tienes pycryptodome instalado

    hex_string = hex(plaintext)[2:]

    # Asegurar longitud par para decodificar

    if len(hex_string) % 2 != 0:

        hex_string = '0' + hex_string

    print("\nEl plaintext convertido a texto es:")

    print(bytes.fromhex(hex_string).decode('utf-8', errors='ignore'))
```
## Referencias