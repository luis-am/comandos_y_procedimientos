El servicio DNS en linux tiene 1 archivo de configuracion ubicado en /etc/named.conf.
Cada dominio administra una zona, y tiene 2 de resolución.
Los archivos de resolución directa e inversa se definen en /etc/named.conf y estan ubicados en /var/named

Deshabilitar NetworkManager
	systemctrl stop NetworkManager
	systemctrl disable NetworkManager
	systemctrl mask NetworkManager

Deshabilitar selinux o colocar en modo permissive, para ver si está corriendo ejecutamos el comando "getenforce". Configurar el archivo:
	path: /etc/selinux/config
 
Instalar los paqutes bind
	yum install bind bind-utils

Iniciar el servicio dns
	systemctl start named
	systemctl enable named

Hacer un backup del archivo de configuracion
	cp /etc/named.conf /etc/named.conf.bk

Consultar la ip de un dominio con un dns específico
	nslookup www.cibertec.edu.pe [DNS server]