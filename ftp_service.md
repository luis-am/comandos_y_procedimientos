### FTP Service

Instalar ftp server.

	sudo apt install vsftpd

Ruta de configuracion:

	vim /etc/vsftpd.conf

Allow anonymous FTP?

	anonymous_enable=YES

Si queremos crear un directorio para ftp, por defecto esta en /srv/ftp.

	sudo mkdir -p /srv/files/ftp

Reiniciar el servicio.

	sudo systemctl restart vsftpd.service

Habilitar usuarios para que puedan cargar archivos.

	write_enable=YES

Enable anonymous users upload

	anon_upload_enable=YES
