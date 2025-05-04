# Configuración Alias SSH 

Para no tener que escribir  
```bash
ssh -p <PUERTO> <USUARIO>@<DOMINIO>
```

Esto te ahorra escribir todo el comando cada vez. Añade esto en tu `~/.ssh/config`:

```ssh-config
Host rpi
    HostName <DOMINIO>
    User <USUARIO>
    Port <PUERTO>
```

Luego solo haces:

```bash
ssh rpi
```
