## Descripcion
There's something in the [building](https://challenge-files.cylabacademy.net/library/5235bfccd8f3cc2d059ee828f774846542f28f7ec66cb4f0c6ceb536c38026d4/buildings.png). Can you retrieve the flag?
## Solucion
### 1. Descargar la imagen

En Kali:

```
wget "https://challenge-files.cylabacademy.net/library/5235bfccd8f3cc2d059ee828f774846542f28f7ec66cb4f0c6ceb536c38026d4/buildings.png"
```

Comprueba que se descargó:

```
ls -l buildings.png
```

### 2. Revisar el archivo

Primero usamos `file`:

```
file buildings.png
```

Debería indicar que es una imagen PNG.

Después podemos revisar si contiene información adicional:

```
strings buildings.png
```

Sin embargo, en este reto la información está **oculta dentro de los píxeles de la imagen**, por lo que `strings` probablemente no será suficiente.

### 3. Analizar la imagen con Stegsolve

Una herramienta clásica para este tipo de retos es **Stegsolve**, que permite analizar diferentes canales de color de una imagen y detectar información escondida mediante técnicas de esteganografía.

Puedes descargarla desde su repositorio correspondiente o utilizar una versión disponible en tu entorno.

Una alternativa más sencilla es utilizar un decodificador de **LSB (Least Significant Bit)**.

La pista:

> "There is data encoded somewhere... there might be an online decoder."

nos da una pista bastante clara: debemos buscar datos codificados dentro de la imagen.

### 4. Utilizar un decoder LSB

Puedes utilizar un decodificador LSB online, por ejemplo **CyberChef**, para analizar la información de la imagen.

También puedes buscar herramientas de análisis de esteganografía que soporten PNG y LSB.

Una herramienta muy útil desde Kali es:

```
zsteg buildings.png
```

Si `zsteg` está instalado, ejecuta:

```
zsteg buildings.png
```

Este comando analiza diferentes canales de bits de la imagen y busca información que pueda estar escondida.

Puedes obtener resultados similares a:

```
b1,r,lsb,xy
b1,rgb,lsb,xy
b2,r,lsb,xy
...
```

Lo interesante son las entradas que indiquen que encontraron texto o datos.

### 5. Extraer la información

En el reto original de **picoCTF 2019 – What Lies Within**, la información está escondida mediante **LSB steganography**.

Una vez localizado el canal correcto, se puede extraer la información oculta y obtener la flag.

```
academy{h1d1ng_1n_th3_b1ts}
```
## Notas adicionales

## Referencias
