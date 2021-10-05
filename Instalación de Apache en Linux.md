# Instalación de Apache en Linux

En el siguiente informe se va a describir los pasos a seguir para instalar un servidor web Apache en una máquina virtual Ubuntu 20.04.03 LTE.

# Requisitos

Será necesario Ubuntu 20.04.03 LTE o cualquier otra distro Linux compatible, acceso a internet y permisos de administrador para el usuario.

# Instalación en local

Antes de comenzar actualizar los repositorios como el sistema operativo.

```console
sudo apt update && sudo apt upgrade
```

Continuar con la instalación de servidor web.Abra una terminal y ejecute el siguiente comando:

```console
sudo apt install apache2
```

Si vuestro equipo ya tiene un proceso corriendo en el puerto 80 lo más seguro es que al instalar el servidor web nos devuelva el siguiente error:

```
(98)Address already in use: AH00072: make_sock: could not bind to address 0.0.0.0:80
```

La forma de solucionarlo es editar el fichero de configuración de puerto de Apache /etc/apache2/ports.conf cambiando el puerto de escucha por el 8080.

```
cambiaer: Listen 80 a Listen 8080 
```

Además, debemos editar la línea a VirtualHost *:8080 en el fichero /etc/apache2/sites-enabled/000-default.conf 

```
cambiar: <VirtualHost: *:80> a <VirtualHost: *:8080
```

Ejecuta los siguientes comandos para reiniciar los servicios_

```console
sudo systemctl restart apache2
sudo service apache2 restart
```

# Ajustar la configuración del Firewall

Usaremos el siguiente comando para verificar los perfiles por defecto para Apache en UFW:

```console
sudo ufw app list
```
Finalizar con un  mensaje similar a:
```console
Available applications:
Apache
Apache Full
Apache Secure
OpenSSH
```

Usaremos el perfil Apache, ya que no será necesario usar una conexión cifrada.

```console
sudo ufw allow Apache
```

Verificamos los perfiles activos:

```console
sudo ufw status
```

Resultado:

  ```console
  Status: active
  To             Action         From
  --             ------         ----
  Apache         ALLOW          Anywhere
  Apache (v6)    ALLOW          Anywhere (v6)
  ```

  Si el Firewall inactivo debes de ejecutar la siguiente instrucción:

  ```console
sudo ufw enable
  ```

  Verificar que el servicio Apache esté ejecutándose correctamente, con el siguiente comando:

```console
sudo systemctl status apache2
```

# Acceso

Para acceder debemos utilizar el navegador introduciendo en la url nuestra dirección IP o mediante localhost.
