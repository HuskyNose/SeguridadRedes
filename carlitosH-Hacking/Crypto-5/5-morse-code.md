## Descripcion
Morse code is well known. Can you decrypt this? Download the file [here](https://challenge-files.cylabacademy.net/library/3728bfa4e8314fddd6b7e9f3fae9cb453b459a0bd4b3a29a9224701152f0cd89/morse_chal.wav).

Wrap your answer with academy{}, put underscores in place of pauses, and use all uppercase.
## Solucion
`.-- .... ....- --... / .... ....- --... .... / ----. ----- -.. / .-- ..--- ----- ..- ----. .... --...`, se obtiene `WH47 H47H 90D W20U9H7`, que es la versión en _leetspeak_ de _"What hath God wrought"_

```
import wave
import struct
import itertools

MORSE_DICT = {
    '.-': 'A', '-...': 'B', '-.-.': 'C', '-..': 'D', '.': 'E',
    '..-.': 'F', '--.': 'G', '....': 'H', '..': 'I', '.---': 'J',
    '-.-': 'K', '.-..': 'L', '--': 'M', '-.': 'N', '---': 'O',
    '--..': 'P', '--.-': 'Q', '.-.': 'R', '...': 'S', '-': 'T',
    '..-': 'U', '...-': 'V', '.--': 'W', '-..-': 'X', '-.--': 'Y',
    '--..': 'Z', '-----': '0', '.----': '1', '..---': '2', '...--': '3',
    '....-': '4', '.....': '5', '-....': '6', '--...': '7', '---..': '8',
    '----.': '9'
}

# 1. Abrir el archivo WAV y extraer muestras en ventanas de 10 ms
with wave.open("morse_chal.wav", "rb") as wav:
    rate = wav.getframerate()
    n_channels = wav.getnchannels()
    sampwidth = wav.getsampwidth()
    n_frames = wav.getnframes()
    raw_data = wav.readframes(n_frames)

# Desempaquetar muestras de 16 bits (signed short)
fmt = f"<{n_frames * n_channels}h"
samples = struct.unpack(fmt, raw_data)[::n_channels]

# 2. Detectar envolvente por ventanas de 10 ms
win_size = rate // 100
envelopes = [
    max(abs(s) for s in samples[i:i + win_size])
    for i in range(0, len(samples) - win_size, win_size)
]
threshold = max(envelopes) * 0.4
binary_signal = [1 if amp > threshold else 0 for amp in envelopes]

# 3. Run-Length Encoding (RLE) de pulsos activos (1) y silencios (0)
runs = [(bit, sum(1 for _ in group)) for bit, group in itertools.groupby(binary_signal)]
# Ignorar silencios al inicio y al final del archivo
while runs and runs[0][0] == 0:
    runs.pop(0)
while runs and runs[-1][0] == 0:
    runs.pop()

# 4. Estimar la unidad base (duración de un punto '.')
on_durations = [length for bit, length in runs if bit == 1]
dot_unit = min(on_durations)

# 5. Reconstruir cadena Morse y traducir a ASCII
morse_str = ""
for bit, length in runs:
    ratio = length / dot_unit
    if bit == 1:
        morse_str += "." if ratio < 2.0 else "-"
    else:
        if ratio > 5.0:
            morse_str += " / "   # Pausa entre palabras
        elif ratio > 2.0:
            morse_str += " "     # Pausa entre letras

decoded_words = []
for word in morse_str.split(" / "):
    decoded_words.append("".join(MORSE_DICT.get(ch, "?") for ch in word.split()))

payload = "_".join(decoded_words)
print(f"[+] Código Morse extraído:\n    {morse_str}\n")
print(f"[+] Flag formato Cylab:   academy{{{payload}}}")
print(f"[+] Flag formato picoCTF: picoCTF{{{payload}}}")
```
## Notas adicionales
**Run-Length Encoding (RLE)** para medir la duración de cada pulso
- **Punto (`.`):** 1 unidad de tiempo Activo.
    
- **Raya (`-`):** 3 unidades de tiempo Activo.
    
- **Espacio entre símbolos de una misma letra:** 1 unidad de Silencio.
    
- **Espacio entre letras:** 3 unidades de Silencio.
    
- **Pausa entre palabras (`_`):** 7 unidades de Silencio.
## Referencias
Gemini Argon Alto, Analizador de Envolvente y Decodificador RLE Morse
![[Pasted image 20261024200314.png]]