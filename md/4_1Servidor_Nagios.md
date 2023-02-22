# 4 Instalación de NAGIOS.
## 4.1 Servidor Nagios.
Empezamos con una actualización del sistema

`sudo apt-update && sudo apt upgrade -y`

Descargamos y descomprimimos Nagios-Core desde el siguiente enlace de [git]( https://github.com/NagiosEnterprises/nagioscore/releases/download/nagios-4.4.6/nagios-4.4.6.tar.gz) con el comando que vemos a continuación

`curl -SL https://github.com/NagiosEnterprises/nagioscore/releases/download/nagios-4.4.6/nagios-4.4.6.tar.gz | tar -xzf - `

Procedemos a instalar Nagios-Core
~~~
cd nagios-4.4.6 

./configure

sudo make all
~~~
Ahora procederemos a crear los usuarios del grupo

`sudo make install-group-users`

`sudo usermod -a -G nagios www-data`

### Instalación del Core

para instalar el core deberemos lanzar el siguiente comando

`sudo make install`

La salida de este último comando nos indica que debemos ejecutar lo siguiente:

`sudo make install-init  #instala el script de inicio en la ruta /lib/systemd/system`

`sudo make install-commandmode #instala y configura permisos`

`sudo make install-config #instala archivos de configuración de ejemplo en /usr/local/nagios/etc`

Ahora debemos instalar Apache

`sudo make install-webconf`

`sudo a2enmod rewrite cgi`

`sudo systemctl restart apache2`

Una vez tenemos instalado Apache, deberemos elegir un tema a instalar.

- instala el tema exfoliation

`sudo make install-exfoliation`

- instala el tema clásico

`sudo make install-classicui`

Como necesitaremos entrar en la web para la monitorización, deberemos crear un usuario de acceso a la misma, para ello lanzamos el siguiente comando

`sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin`

Este comando pedirá contraseña, que se guarda en /usr/local/nagios/etc/htpasswd.users

En este momento deberemos instalar los plugins necesarios para Nagios, para ello nos los descargaremos con el siguiente comando y después de tenerlos descargados, procederemos con la instalación

`curl -SL https://github.com/nagios-plugins/nagios-plugins/releases/download/release-2.4.3/nagios-plugins-2.4.3.tar.gz | tar -xzf -`

`cd nagios-pluggins-2.4.3`

`./configure --with-nagios-user=nagios --with-nagios-group=nagios`

`sudo make install`

Revisamos que los archivos de configuración están correctos con:

`sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`

Si todo es correcto, arrancamos el demonio con:

`sudo systemctl enable --now nagios`
`sudo systemctl status nagios`

Tras este paso podremos tener acceso a Nagios escribiendo la siguiente linea en el buscador que tengamos a mano.

`http://ip.servidor/nagios`

## REGLAS DE FIREWALL

Dependiendo del esquema de red que tengamos será necesario o no aplicar reglas de acceso. Si existe DMZ, si existen subredes, etc., será necesarios implantar reglas de acceso para que nuestro servidor Nagios tenga acceso completo a los siguiente puertos:

- 80/TCP			(HTTP)
- 161/UDP-162/UDP 		(SNMP)
- 22/TCP			(SSH)
- 23/TCP			(TELNET)
- 69/UDP			(TFTP)
- ICMP			(PING)

Realmente los imprescindibles son el SNMP, el SSH y el PING, pero muchos de los pluggins que se pueden instalar en Nagios requieren de los puertos añadidos de la lista.

## [Volver al Inicio.](../README.md)
