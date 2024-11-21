# Comandos nmap

- Testear un servidor

	nmap -sV -sC -p- [IP ADDRESS]
	nmap -sV -sC -p- 192.168.122.1

	-sV: saber la versión
	-sC: ejecutar el script por defecto
	-p-: escanea todos los puertos

- Path de los scripts de nmap

	/usr/share/nmap/scripts/

- Ver los scripts de manera rapida

	locate scripts/[SERVICE]
	locate scripts/ssh
	locate scripts/citrix

- Ejecutar nmap con un script

	nmap --script [SCRIPT NAME] -p [PORT] [IP ADDRESS]
	nmap --script /usr/share/nmap/scripts/rpcap-brute.nse -p 111 192.168.122.1

- Banner grabbing

    nmap -sV --script=banner [IP ADDRESS]
    nmap -sV --script=banner 192.168.122.1

    nmap -sV --script=banner -p21 [IP ADDRESS]
    nmap -sV --script=banner -p21 192.168.122.1

- Enumerar smb service

    nmap --script smb-os-discovery.nse -p445 192.168.122.1
    nmap -A -p445 192.168.122.1

