# tcpdump

## Capturar el tráfico de todas las interfaces

	tcpdump -i any

## Capturar el tráfico de una interface

	tcpdump -i eth0

## Salir luego de recibir la cantidad de paquetes especificados

	tcpdump -i eth0 -c 10

## Leer y analizar un archivo en donde se haya capturado el tráfico

	tcpdump -r file.pcap	

## Escribir la salida en un archivo

	tcpdump -w file.pcap	

## No resolver IPs a nombres

	tcpdump -i eth0 -n

## Verbose

	tcpdump -i eth0 -vvv

## Verbose

	tcpdump -i eth0 -xx

## Muestra solo paquetes TCP

	tcpdump -i eth0 tcp

## Muestra solo paquetes UDP

	tcpdump -i eth0 udp

## Muestra solo paquetes ICMP

	tcpdump -i eth0 icmp

## Muestra solo paquetes IPv4

	tcpdump -i eth0 ip

## Muestra solo paquetes IPv6

	tcpdump -i eth0 ip6

## Muestra solo paquetes ARP

	tcpdump -i eth0 ip6

## Filtrar por IP orígen

	tcpdump src host 10.0.0.1

## Filtrar por IP destino

	tcpdump dst host 10.0.0.1

## Filtrar por orígen o destino

	tcpdump host 10.0.0.1

## Filtrar por MAC orígen

	tcpdump ether src 01:23:45:AB:CD:EF

## Filtrar por MAC destino

	tcpdump ether dst 01:23:45:AB:CD:EF

## Filtrar por MAC origen o destino

	tcpdump ether host 01:23:45:AB:CD:EF

## Filtrar por red de origen

	tcpdump src net 10.0.0.0/27

## Filtrar por red de destino

	tcpdump dst net 10.0.0.0/27

## Filtrar por red de destino u origen

	tcpdump net 10.0.0.0/27

## Filtrar por puerto de origen

	tcpdump src port 22

## Filtrar por puerto de destino

	tcpdump dst port 22

## Filtrar por puerto de destino u origen

	tcpdump port 22

## Filtrar por puerto de origen en el rango de x a y

	tcpdump src portrange 80-400

## Filtrar por puerto de destino en el rango de x a y

	tcpdump dst portrange 80-400

## Filtrar por puerto de destino u origen en el rango de x a y

	tcpdump portrange 80-400

## Filtrar por broadcast ethernet

	tcpdump ether broadcast

## Filtrar por broadcast ethernet

	tcpdump ether broadcast

## Juntar filtros [and]
	
	tcpdump -n 10.0.0.1 && dst port 21
	tcpdump -n 10.0.0.1 and dst port 21

## Juntar filtros [or]
	
	tcpdump -n 10.0.0.1 || dst port 21
	tcpdump -n 10.0.0.1 or dst port 21

## Juntar filtros [not]

	tcpdump -n 10.0.0.1 ! dst port 21
	tcpdump -n 10.0.0.1 not dst port 21
