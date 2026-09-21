## Descripcion
How about trying to match a regular expression

The website is running [here](http://saturn.picoctf.net:65242/).
## Solucion
Utilizaos el siguinte comando para extraer el JavaScript
```
curl -s http://saturn.picoctf.net:65242/ | grep -A 15 "<script>"

```
Nos dara este reultado
```
<script>
        function send_request() {
                let val = document.getElementById("name").value;
                // ^p.....F!?
                fetch(`/flag?input=${val}`)
                        .then(res => res.text())
                        .then(res => {
                                const res_json = JSON.parse(res);
                                alert(res_json.flag)
                                return false;
                        })
                return false;
        }

</script>

```
Se puede ver la pista:
let val = document.getElementById("name").value;
                // ^p.....F!?
Algo em empiece con 'p' y termine 'F', por lo que en el campo de texto solo tenemos que poner picoCTF y la bandera aparecera
## Notas adicionales

## Referencias
