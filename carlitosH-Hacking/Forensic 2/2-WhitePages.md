## Descripcion
I stopped using YellowPages and moved onto WhitePages... but [the page they gave me](https://challenge-files.cylabacademy.net/library/164023ae7e53a7b325e50a82f7cd942427fd0f38084d555c162501500fc475c3/whitepages.txt) is all blank!
## Solucion
### 1. Descarga del archivo

Primero se descargó el archivo `whitepages.txt` proporcionado por el reto:

```
wget "https://challenge-files.cylabacademy.net/library/164023ae7e53a7b325e50a82f7cd942427fd0f38084d555c162501500fc475c3/whitepages.txt"
```

### 2. Inspección del archivo

Se utilizó `xxd` para revisar el contenido hexadecimal del archivo:

```
xxd whitepages.txt | head
```

Al revisar los bytes se identificaron principalmente dos tipos de espacios:

```
20
e2 80 83
```

El byte `20` corresponde a un **espacio normal**, mientras que `e2 80 83` corresponde al carácter Unicode **EM SPACE (`U+2003`)**.

### 3. Identificación del método de ocultamiento

El reto utiliza estos dos caracteres para representar información binaria.

Se estableció una correspondencia:

```
Espacio normal → 1
EM SPACE       → 0
```

De esta manera, los espacios del archivo pueden interpretarse como una secuencia de bits.

### 4. Conversión de los espacios a bits

Se utilizó Python para reemplazar los caracteres por `0` y `1`:

```
python3 -c "data=open('whitepages.txt','rb').read(); data=data.replace(b'\xe2\x80\x83',b'0').replace(b'\x20',b'1'); print(data)"
```

Esto permite visualizar la información oculta como una secuencia binaria.

### 5. Conversión de los bits a texto

Posteriormente, se agruparon los bits de ocho en ocho y cada grupo se convirtió a un carácter ASCII:
## Notas adicionales

## Referencias
