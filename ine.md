## INE comandos

Consultar subdominios

	sublist3r -d [DOMAINNAME]

Instalar y ejecutar amass

	sudo apt install snapd
	sudo apt install amass
	snap run amass | snap run amass -ip -d [DOMAINNAME]

Versión mejorada de ping

	fping -a -s -g [IPSUBNET] 2>/dev/null
		--a: alive
		--s: mostrar estadísticas
		--g: rango de IP

Ping Scan

	nmap -sn [IPRANGE]
		--sn: ping scan, no ports scan

Ping Scan con una lista de IPs

	nmap -sn -iL [FILE]
		--iL: escanea en base a un archivo de texto con las IPs
		--Pn: Trata a todos los hosts online

Mapear los OS de los hosts

	nmap -O [IPRANGE]
		--O: ver el sistema operativo
		--osscan-guess: modo agresivo

Fingerprinting with netcat (solo http)

	nc cibertec.edu.pe 80

Fingerprinting with openssl (https)

	openssl

Fingerprinting with httpprint

	httprint -P0 -h [TARGET] -s [SIGNATURE]
		--P0: avoid pinging the host
		--h: target host
		--s: set the signature file
	ejm: httprint -P0 -h 104.18.8.25 -s /usr/share/httprint/signatures.txt
