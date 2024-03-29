## Comandos de Sophos Firewall

# Verificar si upgrade está disponible para el SSD
	
	system ssd show

# Realizar el upgrade del SSD

	system ssd update

###########################################

# Comandos en [console]

## Obtener la lista de usuarios

	system localusers all_localuser_list show
	sys local all show

## Búsqueda DNS

	dnslookup host [DOMAIN_NAME]
	dnslookup host [DOMAIN_NAME] server [SERVER]
	example: dnslookup host cibertec.edu.pe
	example: dnslookup host cibertec.edu.pe server 8.8.8.8

## Ver los paquetes dropeados tomando en cuenta la interface
	
	drop-packet-capture interface [INTERFACE]
	drop-packet-capture interface PortA
	drop-packet-capture 'host 10.10.10.10'
	drop-packet-capture 'src host 10.10.10.10'
	drop-packet-capture 'dst host 10.10.10.10'
	drop-packet-capture 'net 10.10.10.0/24'
	drop-packet-capture 'src net 10.10.10.0/24'
	drop-packet-capture 'dst net 10.10.10.0/24'
	drop-packet-capture 'port 80'
	drop-packet-capture 'port 80 or port 443'
	drop-packet-capture 'src port 21'
	drop-packet-capture 'dst port 21'
	drop-packet-capture 'host 10.10.10.10 and port 80'
	drop-packet-capture 'host 10.10.10.10 and port not 80'
	drop-packet-capture 'proto ICMP, proto UDP, proto TCP'

## Ver la hora

	show date

## Ver el país en el cual se encuentra una IP
	
	show country-host ip2country ipaddress [X.X.X.X]
	show country-host ip2country ipaddress 1.1.1.1

## Habilitar conexiones remotas ssh

	enableremote port 2222 and serverip [X.X.X.X]

## Deshabilitar conexiones remotas ssh

	disableremote

## Ping con diferentes opciones

	ping sourceip [X.X.X.X] count [X] [X.X.X.X]
	example: ping sourceip 10.10.10.1 count 3 8.8.8.8

## Mostrar las rutas estáticas IPv4 & IPv6
	
	show network static-route
	show network static-route6

## Herramienta 'TCPDUMP'

	tcpdump interface [PORT]	
	tcpdump interface PortA
	tcpdump 'host 10.10.10.10'
	tcpdump 'net 10.10.10.0/24'
	tcpdump 'src net 10.10.10.0/24'
	tcpdump 'dst net 10.10.10.0/24'
	tcpdump 'port 21'
	tcpdump 'src port 21'
	tcpdump 'dst port 21'
	tcpdump 'host 10.10.10.10 and port 21'
	tcpdump 'host 10.10.10.10 and port no 22'
	tcpdump 'proto ICMP'
	tcpdump 'proto UDP'
	tcpdump interface PortB
	tcpdump interface PortB 'port 21'
