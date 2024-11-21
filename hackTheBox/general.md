## Comandos generales

- Extraer versión de web servers, frameworks y aplicaciones.

    whatweb [IP]
    whatweb 192.168.122.1

- Enumeracación a una red entera

    whatweb --no-errors [NETWORK/XX]
    whatweb --no-errors 192.168.122.0/24

- Buscar exploits para un servicio o aplicación en específico

	sudo apt install exploitdb -y
	searchsploit [SERVICE] [N°]
	example: searchsploit openssh 7.2
