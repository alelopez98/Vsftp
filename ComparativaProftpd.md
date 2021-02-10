## VSFTPD Vs PROFTPD

#### VSFTPD
Se trata de un servidor muy seguro, extremadamente rápido y muy estable. Es tan bueno que el FTP de RedHat y Suse usan este servidor FTP.
Fue diseñado e implementado desde el principio con el objetivo que fuera seguro, y gracias a eso, tiene solucionado varios fallos de diseño que su competencia no tiene, como, por ejemplo, no usar en exceso el usuario Root ya que es muy peligroso.

Caracteristicas principales:
- Dispone de configuraciones de IP virtual
- Puedes crear usuarios virtuales
- Puede funcionar en modo operación independiente o inetd
- Puedes establecer límites por IP.
- Es compatible con IPv6.

#### PROFTPD
un servidor FTP que surgió por querer tener un servidor seguro y muy configurable, basado por su admiración hacia el servidor web de Apache por parte de sus creadores.

Características principales:
- Tiene un archivo de configuración principal, que contiene directivas y grupos de directivas que son muy intuitivas si has utilizado el servidor web Apache, ya que se basaron en él para crear Proftpd.
- Dispone de un directorio llamado «.Ftpaccess» que es similar a «.htaccess» de Apache.
- Es muy fácil configurar múltiples servidores FTP virtuales y servicios FTP anónimos.
- Es compatible y tiene soporte de IPv6.
