## Descripcion
Decode this [message](https://challenge-files.cylabacademy.net/library/d825fde6581b1311eafdd403da1cc96f1f98fe3fe84cd71d850310ebb3908088/message.wav) from the moon.
## Solucion
## Análisis de las pistas

### Pista 1: Transmisión de imágenes desde la Luna

Las imágenes de las misiones lunares podían transmitirse mediante una técnica conocida como **SSTV (Slow-Scan Television)**.

SSTV permite transmitir una imagen utilizando una señal de audio. Por lo tanto, aunque el archivo proporcionado sea un `.wav`, el objetivo no es convertir directamente el audio a texto, sino **decodificar la señal de audio para recuperar una imagen**.

El proceso esperado es:

```
message.wav
     ↓
Señal SSTV
     ↓
Decodificador SSTV
     ↓
Imagen
     ↓
Flag
```

---

## 3. Análisis de la segunda pista

La segunda pista pregunta por la mascota de **Carnegie Mellon University (CMU)**.

La mascota de CMU es **Scotty**, un Scottish Terrier.

Esto da una pista sobre el modo de SSTV que debemos utilizar:

```
Scotty
   ↓
Scottie
   ↓
Scottie 1
```

Por lo tanto, el modo de recepción que debemos buscar es **Scottie 1**.

---

## 4. Descarga del archivo

Primero se descarga el archivo `message.wav` desde el enlace proporcionado por el reto.

En Kali Linux se puede utilizar:

```
wget "https://challenge-files.cylabacademy.net/library/d825fde6581b1311eafdd403da1cc96f1f98fe3fe84cd71d850310ebb3908088/message.wav"
```

Después se verifica que el archivo exista:

```
ls -l message.wav
```

También podemos comprobar el tipo de archivo:

```
file message.wav
```

El resultado debe indicar que se trata de un archivo de audio WAV.

---

## 5. Instalación del decodificador SSTV

Se utiliza la herramienta `sstv`, que permite decodificar señales SSTV almacenadas en archivos de audio.

Primero se actualizan los repositorios:

```
sudo apt update
```

Después se instala la herramienta:

```
sudo apt install sstv
```

---

## 6. Decodificación del archivo

Una vez instalada la herramienta, se ejecuta:

```
sstv -d message.wav -o moonwalk.png
```

Donde:

- `-d` indica que se va a decodificar el archivo.
- `message.wav` es el archivo de audio proporcionado por el reto.
- `-o moonwalk.png` indica el nombre de la imagen de salida.

La herramienta analiza la señal de audio y detecta el formato SSTV utilizado.

El modo esperado es:

```
Scottie 1
```

Después de finalizar la decodificación se obtiene:

```
moonwalk.png
```

---

## 7. Visualización de la imagen

Para abrir la imagen desde Kali Linux se puede utilizar:

```
xdg-open moonwalk.png
```

También se puede abrir directamente desde el explorador de archivos.

La imagen obtenida contiene el mensaje transmitido mediante SSTV.

En caso de que la imagen aparezca con una orientación incorrecta, se puede rotar para poder leer correctamente el contenido.

---

## 8. Resultado

Después de decodificar la señal SSTV utilizando el modo **Scottie 1**, se obtiene la imagen que contiene la bandera del reto.

La flag obtenida es:

```
picoCTF{beep_boop_im_in_space}
```
## Notas adicionales

## Referencias
