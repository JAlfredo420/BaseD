# Configuración de Servidores y Gestión de Bases de Datos

## Configuración de un Dominio en Hostinger

Para vincular un dominio personalizado con el panel de control Hestia en Hostinger, sigue estos pasos:

### 1️⃣ Registro y Configuración del Dominio

1. Accede a tu cuenta en Hostinger.
2. Dirígete a la sección *Dominios* y selecciona *Registrar un dominio nuevo*.
3. Introduce el nombre del dominio deseado (ejemplo: tusitio.com).
4. Finaliza el pago y espera la activación del dominio (este proceso puede tardar hasta 24 horas).

Imagen 1: Proceso de registro de dominio

### 2️⃣ Modificación de los Servidores de Nombres (DNS)

1. En el *Panel de Control* de Hostinger, ve a *Dominios > Administrar*.
2. En *Nameservers (DNS), selecciona **Usar servidores de nombres personalizados*.
3. Configura los servidores DNS apuntando hacia tu VPS en Oracle Cloud:
```
   
   ns1.tusitio.com
   ns2.tusitio.com
 ```  

4. Guarda los ajustes y espera la propagación de DNS (este proceso puede tardar varias horas).

Imagen 2: Modificación de DNS en Hostinger

## 3️⃣ Asociar el Dominio en Hestia Control Panel

Para reemplazar localhost por tu dominio en Hestia, sigue estos pasos:

1. Conéctate a tu VPS a través de *SSH* como usuario root:
   bash
   ```
   ssh root@<IP_DEL_SERVIDOR>
   ```

Imagen 3: Instalación de Hestia mediante línea de comandos

## Instalación de Hestia

👾[Hestia install](https://hestiacp.com/install)

Para configurar Hestia en tu servidor, ejecuta el siguiente comando en la terminal:
```
bash
cd /usr/local/hestia/bin/
v-change-sys-hostname tusitio.com
v-add-letsencrypt-host
```
Imagen 4: Configuración de Hestia mediante terminal

## Verificación de la Propagación del DNS

Para confirmar que el dominio se ha propagado correctamente, utiliza la herramienta siguiente.

🌍[Esta es una herramienta para verificar](https://www.whatsmydns.net/)

1. Accede a la plataforma en línea.
2. Escribe tu dominio (tusitio.com).
3. Selecciona el tipo de registro DNS (A, CNAME, MX, etc.).
4. Pulsa en *Buscar* para verificar la propagación en servidores globales.

Imagen 5: Verificación de propagación DNS

## Instalación de Apache y PHP en Oracle Cloud
♨️[Te puedes ayudar de la siguiente paguina](https://docs.oracle.com/en-us/iaas/developer-tutorials/tutorials/apache-on-ubuntu/01oci-ubuntu-apache-summary.htm#set-up-apache-php)
### Acceder a la Máquina Virtual

1. Entra a Oracle Cloud [Oracle Cloud](https://www.oracle.com/cloud/sign-in.html?redirect_uri=https%3A%2F%2Fcloud.oracle.com%2F)
2. Escoge la instancia previamente creada.
3. Ubica la dirección *Public IP Address* y guárdala.

### Conectar a la Máquina vía SSH

Ejecuta el siguiente comando en tu terminal:
bash
```
ssh -i <tu-clave-privada.key> ubuntu@<IP_DE_LA_INSTANCIA>
```

Imagen 6: Acceso SSH a la instancia

### Instalación de Apache y PHP

Actualiza los paquetes e instala Apache con:
```
bash
sudo apt update
sudo apt -y install apache2
```

Inicia Apache y revisa su estado con:
```
bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

Configura el firewall para permitir tráfico HTTP:
```
bash
sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 80 -j ACCEPT
sudo netfilter-persistent save
```

Imagen 7: Instalación de Apache y PHP

## Comprobación del Servidor

Para verificar que Apache está funcionando, accede a tu dirección IP en un navegador agregando /index.html.

También puedes comprobar la ejecución de PHP creando un archivo con el siguiente código:
```
php
<?php
phpinfo();
?>
```

Guarda este archivo en /var/www/html/ y ábrelo desde el navegador.

Imagen 8: Verificación de Apache con PHP

## Pasos para Configurar HTTPS en HestiaCP
### 1️⃣ Acceder a HestiaCP
### Ve a https://<"IP">:8083/ e inicia sesión como admin.

* 2️⃣ Agregar un Dominio a HestiaCP
* En el panel de control, ve a Web > Añadir dominio.

* Escribe tu dominio (Ejemplo: midominio.com).

* Marca la opción Habilitar Soporte SSL.

* Marca la opción Usar Let’s Encrypt.

* Haz clic en Guardar.

### 3️⃣ Configurar el Certificado SSL Manualmente (Opcional)
Si la opción Let’s Encrypt no funciona automáticamente, puedes activarlo por SSH con los siguientes comandos:
```
v-add-web-domain-ssl "usuario de hestia" midominio.com
v-add-letsencrypt-domain "usuario de hestia" midominio.com
```
### Buscador de Paguina usando HTTPS
