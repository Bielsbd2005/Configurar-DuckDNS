Para no tener que escribir  
```bash
ssh -p 2222 biel@raspberrybiel.duckdns.org
```

Esto te ahorra escribir todo el comando cada vez. Añade esto en tu `~/.ssh/config`:

```ssh-config
Host rpi
    HostName raspberrybiel.duckdns.org
    User pi
    Port 2222
```

Luego solo haces:

```bash
ssh rpi
```
