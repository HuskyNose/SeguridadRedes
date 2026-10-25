## Descripcion
We found a leak of a blackmarket website's login credentials. Can you find the password of the user `cultiris` and successfully decrypt it? Download the leak [here](https://challenge-files.cylabacademy.net/library/7f760cee144ac7237469fd6bfab7c748d6f1d101ca47c101187ca7d8f5c721f0/leak.tar).

The first user in `usernames.txt` corresponds to the first password in `passwords.txt`. The second user corresponds to the second password, and so on.
## Solucion

import codecs

with open("usernames.txt", "r", encoding="utf-8") as u_file, \
     open("passwords.txt", "r", encoding="utf-8") as p_file:

    # Empareja usuario y contraseña línea por línea
    for linea, (user, pwd) in enumerate(zip(u_file, p_file), start=1):
        if user.strip() == "cultiris":
            cifrado = pwd.strip()
            flag = codecs.decode(cifrado, "rot_13")
            print(f"[+] Usuario encontrado en la línea: {linea}")
            print(f"[+] Contraseña cifrada: {cifrado}")
            print(f"[+] Flag descifrada:    {flag}")
            break
## Notas adicionales

## Referencias
