### A) Version Instalada
![imagen](imagenes/aversion.JPG) 
### B) Usuarios Creados en la Instalación
* Vamos a ver que usuarios y grupos se han creado.
* Con el comando:  
```
$ cat /etc/passwd
```
* Vemos que se ha creado:  
![imagen](imagenes/usuario.jpg)  
* Con el comando:  
```
$ cat /etc/group
```
   * vemos que se ha creado:  

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
### E) Acceso al servidor FTP: usuarios del sistema
### F) Acceso al servidor FTP: anónimo tiene solo permiso de lectura en su directorio de trabajo
### G) Acceso al servidor FTP: anónimo tiene permiso de escritura en el directorio sugerencias, que es un subdirectorio de su directorio raíz.
### H) Acceso al servidor FTP: Creación de usuarios virtuales.
### I) Acceso seguro al servidor FTP
