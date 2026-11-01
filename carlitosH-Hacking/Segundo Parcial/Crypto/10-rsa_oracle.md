## Descripcion
Can you abuse the oracle?

An attacker was able to intercept communications between a bank and a fintech company. They managed to get the [message](https://challenge-files.cylabacademy.net/library/1b39f2751ae1461b00924da90f25e9803b0cee634d2244dccf6554277057994e/secret.enc) (ciphertext) and the [password](https://challenge-files.cylabacademy.net/library/1b39f2751ae1461b00924da90f25e9803b0cee634d2244dccf6554277057994e/password.enc) that was used to encrypt the message.
## Solucion
```

import socket
import hashlib
from pathlib import Path

from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad


HOST = "chatelaine.cylabacademy.net"
PORT = 11194

PASSWORD_CIPHER = int(
    "3866059118128440816066897401856426000966295118699899417550986956938429514754327731737414991842543326348611940913710191848472878865665656456524988060185143"
)


class Oracle:
    def __init__(self, sock):
        self.sock = sock
        self.buffer = b""

    def until(self, marker):
        while marker not in self.buffer:
            data = self.sock.recv(4096)

            if not data:
                raise ConnectionError(
                    "El servidor cerro la conexion."
                )

            self.buffer += data

        pos = self.buffer.index(marker) + len(marker)

        result = self.buffer[:pos]
        self.buffer = self.buffer[pos:]

        return result

    def line(self):
        while b"\n" not in self.buffer:
            data = self.sock.recv(4096)

            if not data:
                raise ConnectionError(
                    "No se recibio la respuesta esperada."
                )

            self.buffer += data

        result, self.buffer = self.buffer.split(b"\n", 1)

        return result.strip()


def recover_password():

    print("[+] Conectando con el oraculo RSA...")

    with socket.create_connection(
        (HOST, PORT), timeout=15
    ) as sock:

        sock.settimeout(15)
        oracle = Oracle(sock)

        # Esperar el menu
        oracle.until(b"E --> encrypt D --> decrypt.")

        # Solicitar el cifrado del numero 2
        sock.sendall(b"E\n")

        oracle.until(b"keysize): ")

        # Enviar el byte 0x02, no el caracter ASCII '2'
        sock.sendall(b"\x02\n")

        oracle.until(b"ciphertext (m ^ e mod n)")

        c2 = int(oracle.line())

        print("[+] Ciphertext de 2 obtenido.")

        # Esperar el siguiente menu
        oracle.until(b"E --> encrypt D --> decrypt.")

        # Calcular el ciphertext modificado
        modified_cipher = PASSWORD_CIPHER * c2

        # Solicitar el descifrado
        sock.sendall(b"D\n")

        oracle.until(b"decrypt: ")

        sock.sendall(
            str(modified_cipher).encode() + b"\n"
        )

        oracle.until(
            b"decrypted ciphertext as hex (c ^ d mod n):"
        )

        decrypted_hex = oracle.line().decode().strip()

        # Convertir el hexadecimal a entero
        doubled_password = int(decrypted_hex, 16)

        if doubled_password % 2 != 0:
            raise ValueError(
                "El resultado no es par. "
                "Comprueba la respuesta del oraculo."
            )

        # Deshacer el factor multiplicativo
        password_number = doubled_password // 2

        password_bytes = password_number.to_bytes(
            (password_number.bit_length() + 7) // 8,
            "big"
        )

        password = password_bytes.decode("utf-8")

        print("[+] Contraseña recuperada:", password)

        return password_bytes


def derive_key(password, salt, digest):

    result = b""
    previous = b""

    while len(result) < 48:

        previous = hashlib.new(
            digest,
            previous + password + salt
        ).digest()

        result += previous

    return result[:32], result[32:48]


def decrypt_message(password):

    print("[+] Leyendo secret.enc...")

    data = Path("secret.enc").read_bytes()

    if not data.startswith(b"Salted__"):
        raise ValueError(
            "El archivo no tiene el encabezado Salted__."
        )

    salt = data[8:16]
    ciphertext = data[16:]

    if not ciphertext or len(ciphertext) % 16 != 0:
        raise ValueError("Tamano incorrecto del ciphertext.")

    # Probar derivacion tradicional de OpenSSL
    for digest in ("sha256", "md5"):

        key, iv = derive_key(password, salt, digest)

        decrypted = AES.new(
            key, AES.MODE_CBC, iv
        ).decrypt(ciphertext)

        try:
            plaintext = unpad(decrypted, AES.block_size)
            message = plaintext.decode("utf-8")

            if message.isprintable() or "\n" in message:
                print("[+] Metodo utilizado:", digest)
                return message

        except (ValueError, UnicodeDecodeError):
            pass

    # Alternativa: OpenSSL con PBKDF2
    material = hashlib.pbkdf2_hmac(
        "sha256", password, salt, 10000, dklen=48
    )

    key = material[:32]
    iv = material[32:48]

    decrypted = AES.new(
        key, AES.MODE_CBC, iv
    ).decrypt(ciphertext)

    plaintext = unpad(decrypted, AES.block_size)

    return plaintext.decode("utf-8")


if __name__ == "__main__":

    password = recover_password()

    print("\n[+] Iniciando descifrado AES...")

    flag = decrypt_message(password)

    print("\n" + "=" * 50)
    print("MENSAJE DESCIFRADO:")
    print("=" * 50)

    print(flag)

```
## Notas adicionales

## Referencias