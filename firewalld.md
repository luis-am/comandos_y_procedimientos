## Comandos 'Firewall'

Listar toda la configuración por defecto de firewalld (zona pública por defecto).

	sudo firewall-cmd --list-all

Listar todas las zonas.

	sudo firewall-cmd --list-all-zones

Listar la configuración de una zona en específico.
	
	sudo firewall-cmd --list-all --zone=[ZONA]

Listar las zonas actualmente asignadas a cada interface.
	
	sudo firewall-cmd --get-active-zones

Ver todas las zonas disponibles.

	sudo firewall-cmd --get-zones

Poner por defecto una zona por defecto, en este caso por ejemplo estoy poniendo la zona de 'home'

	sudo firewall-cmd --set-default-zone=home

Establecer una interface a una zona en específico, en el ejemplo se muestra que estamos asignando la interface enp42s0 a la zona 'home', recordar que por defecto está en la zona 'public'.
	
	sudo firewall-cmd --zone=home --change-interface=[INTERFACE] --permanent

Ver todos los servicios predefinidos.

	sudo firewall-cmd --get-services

Permitir el tráfico de un servicio.

	sudo firewall-cmd --add-service=[SERVICE] --permanent
	sudo firewall-cmd --reload

Eliminar un servicio.

	sudo firewall-cmd --remove-service=[SERVICE] --permanent
	sudo firewall-cmd --reload

Agregar un puerto.

	sudo firewall-cmd --add-port=[]/tcp --permanent
	sudo firewall-cmd --add-port=[]/udp --permanent
	sudo firewall-cmd --reload

Eliminar un puerto.

	sudo firewall-cmd --remove-port=[]/tcp --permanent
	sudo firewall-cmd --remove-port=[]/udp --permanent
	sudo firewall-cmd --reload
