### Servicio Samba

Instalando el servicio samba.

	sudo apt install samba

Esta es la ruta del archivo de configuración de samba.

	vim /etc/samba/smb.conf

Ya dentro del grupo editamos el 'workgroup'.

	workgroup = MIGRUPO

Aquí se muestra un ejemplo básico.

	[share]
	comment = comentario del directorio
	path = /home/luisam/share
	browsable = yes
	guest ok = yes | no (usuarios sin contraseña)
	read only = no
	valid users = [username1] [username2]
	create mask = 0755

Crear la carpeta a la que se va a compartir, y cambiarle los permisos.

	sudo mkdir -p /home/luisam/share
	sudo chown nobody:nogroup /srv/samba/share/

Reiniciar los servicios de samba para habilitar la nueva configuracion.

	sudo systemctl restart smbd.service nmbd.service

Verificar la configuracion de smb.conf.

	sudo testparm

Crear usuarios para samba.

	sudo useradd [username] -s /sbin/nologin
	sudo smbpasswd -a [username]

Instalar cliente samba

	sudo yum install samba-client

Conectarse desde un cliente linux

	smbclient -U [username] //x.x.x.x/sharedFiles
