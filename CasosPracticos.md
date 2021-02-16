### A) Version Instalada
![imagen](imagenes/aversion.JPG) 
### B) Usuarios Creados en la Instalación
Vamos a ver que usuarios y grupos se han creado.
Con el comando:  
```
$ cat /etc/passwd
```
Vemos que se ha creado:  
![imagen](imagenes/usuario.jpg)  
Con el comando:  
```
$ cat /etc/group
```
vemos que se ha creado:  
![imagen](imagenes/grupo.jpg)  
### C) Servicio Asociado
* El servicio es vsftpd.service
```
$ systemctl status vsftpd
```
```
$ systemctl restart vsftpd
```
```
$ systemctl stop vsftpd
```
### D) Ficheros de Configuración
El fichero de configuracion se encuentra en /etc y es:
```
/etc/vsftpd.conf
```
Las directivas mas importantes son:
- **local_enable** = Al estar activada, los usuarios locales pueden conectarse al sistema.
- **anon_root** = Especifica el directorio al cual vsftpd cambia luego que el usuario anónimo se conecta.
- **ftp_username** = Especifica la cuenta del usuario local (listada en /etc/passwd) utilizada por el usuario FTP anónimo. El directorio principal especificado en /etc/passwd para el usuario es el directorio raíz del usuario FTP anónimo.
- **chmod_enable** = Cuando está activada, se permite el comando FTP SITE CHMOD para los usuarios locales. Este comando permite que los usuarios cambien los permisos en los archivos.
- **chroot_list_enable** = Cuando está activada, se coloca en una prisión de chroot a los usuarios locales listados en el archivo especificado en la directriz chroot_list_file.
- **chroot_local_user** = Si está activada, a los usuarios locales se les cambia el directorio raíz (se hace un chroot) a su directorio principal luego de la conexión.
- **local_umask=022** = Esta directiva nos permite habilitar los permisos nuevos cuando copiemos datos al servidro FTP, por defecto el umask es 077 pero podremos modificarlo por el valor que nosotros queramos, 022 es el umask más utilizado en otros servidores FTP.  
- **[Todas las Directivas](https://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-rg-es-4/s1-ftp-vsftpd-conf.html)**
### E) Acceso al servidor FTP: usuarios del sistema
Antes de empezar nos crearemos un nuevo usuario y le cambiaremos los permisos  
![imagen](imagenes/usuario1.jpg)  
Tambien cambiaremos la contraseña  
```
passwd alejandro
```
Le damos permisos  
```
chmod -R 777 /etc/alejandro
```
Ahora tocaremos el fichero de configuración de vsftpd.conf, pondremos listen en modo YES  
![imagen](imagenes/vsftpdconf.JPG)  
 Y añadiremos la siguiente linea  
 ![imagen](imagenes/vsftpdconf1.JPG)  
 - Finalmente nos conectamos desde filezilla  
 ![imagen](imagenes/conexionfilezilla.JPG) 
### F) Acceso al servidor FTP: anónimo tiene solo permiso de lectura en su directorio de trabajo 
Vamos a editar el fichero /etc/vsftpd.conf. Cambiamos la siguiente linea a YES. Para permitir acceder como usuario anonimo.    

 ![imagen](imagenes/anonimo.jpg)    
   
Luego reiniciamos el servicio
```
systemctl restart vsftpd
```
Y desde filezilla hacemos las comprobaciones.
Primero nos conectamos.  
  
 ![imagen](imagenes/anonimo2.jpg)   
 
Intentamos subir un archivo, y como vemos no nos deberia dejar.  
  
 ![imagen](imagenes/anonimo3.jpg) 
### G) Acceso al servidor FTP: anónimo tiene permiso de escritura en el directorio sugerencias, que es un subdirectorio de su directorio raíz.  
Vamos a darle permisos al directorio ftp  
```
chown ftp:nogroup /srv/ftp
```
Luego creamos la carpeta sugerencias que tambien le daremos los permisos
```
chown ftp:nogroup /srv/ftp/sugerencias
```
A continuacion editamos el fichero /etc/vsftpd.conf y añadimos las siguientes directivas:  
  
 ![imagen](imagenes/anonimo6.jpg)  
Ahora entramos en filezilla desde el host y comprobamos que puede acceder y desde ftp no puede subir archivos
  
![imagen](imagenes/anonimo4.jpg)  
 Pero desde sugerencias si  
   
![imagen](imagenes/anonimo5.jpg)
### H) Acceso al servidor FTP: Creación de usuarios virtuales.  
Para este paso primero tenemos que instalar el siguiente paquete.  
```
apt install libpam-pwdfile
```
1) Creamos un fichero donde vamos a guardar los usuarios heidi y pedro  
  
![imagen](imagenes/virtuales.jpg)  
2) En el fichero /etc/pam.d/vsftpd comentamos la linea por defecto y añadimos nuestra configuracion.  
  
![imagen](imagenes/virtuales2.jpg)  
3) Con el siguiente comando creamos los usuarios virtuales.  
```
useradd --home /home/vsftpd --gid nogroup -m --shell /bin/bash vsftpd
```
4) Dentro del directorio /etc/vsftpd_user_conf creamos los ficheros pedro y heidi con la siguiente configuracion
- heidi  
![imagen](imagenes/heidi.jpg)  
- Pedro  
![imagen](imagenes/pedro.jpg)  
5) Finalmente creamos los directorios heidi y pedro en /srv/ftp y les damos los permisos  
  
![imagen](imagenes/finalvirtuales.jpg)  
6) Entramos como heidi para comprobar.  
  
![imagen](imagenes/comprobacion.jpg) 
### I) Acceso seguro al servidor FTP
