# 2  La herramienta NAGIOS
## 2.2.- PLATAFORMAS Y REQUISITOS

Nagios sólo está disponible para su instalación en las distribuciones Linux de 64 bits siguientes:

- RHEL 7/8/9
- CentOS 7/Stream 8/Stream 9
- Oracle Linux 7/8
- Debian 9/10/11
- Ubuntu 16/18/20/22 (LTS)

Los requerimientos mínimos de instalación son:

- Procesador a 1 GHz 
- 1 GB RAM
- 8 GB de espacio en HD

Los requerimientos recomendados son:

- Procesador a más de 2 GHz
- 2 GB RAM
- 40 GB de espacio en HD
- Sistema de discos redundante (RAID)

Nagios no ofrece soporte para fallos de paquetería durante la instalación, para ninguna distribución, pero no ofrece ningún tipo de soporte (ni de instalación ni de 
funcionamiento) para maquinas virtuales de Azure

En máquinas físicas de Windows no se puede instalar. Nagios ofrece máquinas virtuales precargadas para abrirlas con VMWare o Hyper-V en sistemas Windows

## 2.3.- AGENTES

Nagios monitorizará por SNMP aquellos equipos Linux, Windows, Mac o Android que tengan un cliente específico instalado, pero también puede comunicarse, 
a través de ese mismo protocolo SNMP, con dispositivos físicos tales como switches, routers, impresoras, SAIs...

Supervisa elementos, que se definen en monitorización como un aspecto único del dispositivo que se está monitorizando, que devuelve una o más piezas de información

La monitorización puede establecerse de manera proactiva (pull) sondeando dispositivos de forma programada, o de manera pasiva (push) en la que el servidor espera que los agentes 
envíen actualización de su estado, en base a una frecuencia predeterminada

Esta información recopilada podemos guardarla, para evaluarla y estudiarla en un almacén de datos, o recopialrla, evaluarla, actuar en función de lo que se requiera y luego
olvidarla

Los agentes activos o los pasivos nos permiten contralar, fundamentalmente, la disponibilidad del dispositivo (si se puede acceder al mismo), 
fallos en el mismo (detección, aislamiento, correción y registro de eventos) o rendimiento (eficiencia, utilizacion, tasas de error, tiempo de respuesta...)