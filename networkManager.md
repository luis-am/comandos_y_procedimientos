## Como configurar el servicio de NetworkManager

La ruta por defecto en debian para la configuración de interfaces es

	/etc/network/interfaces

Aquí un ejemplo de una configuraión básica

	# The loopback network interface
	auto lo
	iface lo inet loopback

	# The primary network interface
	allow-hotplug [INTERFACE]
	iface [INTERFACE] inet [static|dhcp]
	address [x.x.x.x]
	netmask [x.x.x.x]
	gateway [x.x.x.x]
	dns-nameservers [x.x.x.x]

Instalamos primero el package 'network-manager'

	sudo apt install network-manager

Para que NetworkManager se encargue de gestionar la configuración del archivo /etc/network/interfaces, poner 'true' en la linea, por defecto está en 'false'.

	[ifupdown]
	managed=true
