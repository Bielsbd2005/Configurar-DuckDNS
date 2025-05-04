# Configurar DuckDNS

1. **Regístrate y crea tu subdominio en DuckDNS**  
   - Ve a https://www.duckdns.org/ y regístrate.  
   - En la sección **Domains** añade un nuevo dominio, por ejemplo `mi-pi`.  
   - Copia el token que te proporcionan; lo necesitarás para la actualización.

2. **Crea el script de actualización en la Pi**  

   En tu Raspberry Pi, abre una terminal y ejecuta:  
   ```bash
   mkdir -p ~/duckdns
   cd ~/duckdns
   ```

   Crea el archivo `duck.sh`:  
   ```bash
   cat > duck.sh << 'EOF'
   #!/bin/bash
   URL="https://www.duckdns.org/update?domains=mi-pi&token=TOKEN&ip="
   curl -k "$URL" > duck.log 2>&1
   EOF
   ```

   Hazlo ejecutable:  
   ```bash
   chmod +x ~/duckdns/duck.sh
   ```

   Reemplaza `mi-pi` por el nombre de tu dominio DuckDNS y `TOKEN` por el token que copiaste en el paso anterior.

3. **Programa la actualización automática con cron**  

   Para que tu IP pública se actualice automáticamente cada 5 minutos:  
   ```bash
   crontab -e
   ```  
   Y añade esta línea al final:  
   ```bash
   */5 * * * * /home/pi/duckdns/duck.sh
   ```  
   > **Nota:** DuckDNS requiere al menos una petición cada 30 minutos para que tu dominio siga activo. Con 5 minutos tienes margen amplio.

4. **Verifica que funciona**  

   Tras unos minutos, comprueba el log:  
   ```bash
   cat ~/duckdns/duck.log
   ```  
   Deberías ver algo como `OK` o tu IP. También puedes hacer:  
   ```bash
   ping -c1 mi-pi.duckdns.org
   ```  
   y ver que responde con tu IP pública.
