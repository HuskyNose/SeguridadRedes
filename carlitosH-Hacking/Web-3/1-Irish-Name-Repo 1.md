## Descripcion
Do you think you can log us in? Try to see if you can login!

[http://fickle-tempest.picoctf.net:50847](http://fickle-tempest.picoctf.net:50847/).
## Solucion
Escribe exactamente esto: `' OR 1=1;--` _¿Por qué funciona?_ La comilla simple cierra la cadena del programador. El `OR 1=1` inyecta una condición que siempre es verdadera. El punto y coma y los guiones (`;--`) le dicen al motor de la base de datos que ignore el resto de la línea (como la validación de la contraseña).
## Notas adicionales

## Referencias
