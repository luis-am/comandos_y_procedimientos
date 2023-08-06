## Servicio de Firewall

#### ufw - Uncomplicated Firewall

Habilitar, deshabilitar.

	sudo ufw enable
	sudo ufw disable

Abrir un puerto por ejemplo.

	sudo ufw allow 22

Abrir puerto con el siguiente formato.

	sudo ufw insert 1 allow 80

Denegar un puerto.

	sudo ufw deny 22

Eliminar una regla.

	sudo ufw delete deny 22

Crear regla para un especifico host.

	sudo ufw allow proto tcp from 192.168.0.2 to any port 22

Ver el estado del ufw.

	sudo ufw status

Ver la informacion verbose.

	sudo ufw status verbose

Ver la informacion enumerada.

	sudo ufw allow 67

