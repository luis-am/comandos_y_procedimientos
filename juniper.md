## Comandos Juniper

> Router Juniper

> username: root

> password: root123

<br>

- \% == shell mode

- \> == operational mode

- \#  == configuration mode

<br>

Help 

	help topic [command]
	help reference [command]
	help apropos [abc]
	help tip cli

Establecer el ancho del cli 

	screen width set to 128

Crear un nuevo usuario 

	edit system login
	edit user [usuario]
	set full-name "[nombre]"
	set class super-user
	set authentication plain-text-password
	commit

Ver la hora en el router 

	show system uptime

Cambiar la zona regional 

	set system time-zone America/Lima

Ver la tabla de enrutamiento 

	show route

Ver la tabla de enrutamiento 

	show route detail

Ver las interfaces 

	show interfaces terse

Parecido al do de cisco 

	run [comando]

Ver la comparativa de los cambios antes del commit 

	show | compare

	commit
	commit and-quit
	commit confirmed [#min]
	configure or edit
	show system commit revision detail
	show configuration | compare rollback
	set system max-configurations-on-flash [0-49]

Asignar password al root 

	set system root-authentication plain-text-password

Configurar hostname 

	set system host-name [abc]

Ver los cambios hechos 

	show system commit

Ver la version del equipo 

	show version

Ver la informacion del sistema 

	show system information

Ver configuracion en display set 

	show configuration | display set

Ver la configuracion completa de una interface

	show interfaces ge-0/0/0 extensive

Math con el output 

	show interfaces terse | match inet

Configuracion basica  (si se tiene dos direcciones se prefiere la menor a menos que pongamos preferred)

	set system host-name [abc]
	set system time-zone America/Lima
	set system root-authentication plain-text-password
	edit interfaces ge-0/0/2 unit 0 family inet address x.x.x.x/24
	edit interfaces ge-0/0/2 unit 0 family inet address x.x.x.x/24 preferred
	edit interfaces ge-0/0/2 unit 0 family inet address x.x.x.x/24 primario (si en caso es de otra subred)
	set interfaces ge-0/0/2 gigether-options no-auto-negotiation
	edit interfaces ge-0/0/2
		set link-mode full-duplex
		set speed 1g
		set mtu 9192

Guardar un archivo de backup 

	request system configuration rescue save

Guardar un archivo de backup 

	request system configuration rescue delete

Regresar a la configuracion de rollback 

	rollback rescue

Cargar una configuracion 

	load override [file]
