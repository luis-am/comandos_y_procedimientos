## Comandos de Windows

Mezclador de volumen

	sndvol

Administrador de sonido y audio

	mmsys.cpl

Administrador de usuarios y grupos locales

	lusrmgr.msc

Administrador de equipo

	compmgmt.msc

Configuracion regional

	intl.cpl

Conexion escritorio remoto

	mstsc

Programador de tareas

	taskschd.msc

Visor de eventos

	eventvwr.msc

Programas y caracteristicas

	appwiz.cpl

Propiedades del sistema

	sysdm.cpl

Consola de herramientas administrativas

	mmc
	control admintools

Tiempo y hora

	timedate.cpl

Limpieza de disco

	cleanmgr

Desfragmentador de discos

	dfrgui

Propiedades del escritorio

	desk.cpl
	control desktop

Propiedades de internet

	inetcpl.cpl

Configuracion del sistema

	msconfig

Informacion del sistema

	msinfo32

Administrador de adaptadores de red

	ncpa.cpl

Administrador de firewall

	firewall.cpl

Administrador de servicios

	services.msc

Mapa de caracteres (caracteres especiales)

	charmap

Centro de accesibilidad

	utilman
	control access.cpl

Calculadora

	calc

Items de panel de control

	control

Administrador de dispositivos

	devmgmt.msc

Directx herramienta de diagnostico

	dxdiag

Abre carpeta documentos

	documents

Abre carpeta descargas

	downloads

Abre carpeta imagenes

	pictures

Opciones de explorador de archivos, carpetas

	control folders

Vista previa de fuentes

	control fonts
	fonts

Controles de juego

	joy.cpl

Editor de politicas de grupo local

	gpedit.msc

Propiedades de teclado

	control keyboard

Abre word

	winword

Abre excel

	excel

Abre power point

	powerpnt

Abre paint

	mspaint

Propiedades de mouse

	control mouse

Abre el bloc de notas

	notepad

Teclado en pantalla

	osk
	ctrl + win + o

Dispositivos e impresoras

	control printers

Editor de regitros

	regedit
	regedt32.exe

Monitor de recursos

	resmon

Restaurar sistema

	rstrui

Administrador de tareas

	taskmgr

Configuracion de firewall avanzado

	wf.msc

Lupa

	magnify

Version de windows

	winver

Abre wordpad

	write

Abre la carpeta usuarios

	..

Abre la carpeta del usuario actual

	.

Abre el directorio C:\

	\

Abre la carpeta videos

	videos

Control de actualizaciones

	control update

Backup y restauracion

	sdclt

Calibracion, color del display

	dccw

Activar desactivar caracteristica opcionales

	optionalfeatures
	
---

### Comandos CMD

Ver nombre del equipo

	hostname

Ver usuario actual

	whoami

Ver la etiqueta del volumen

	vol

Ver la version de windows

	ver

Ver la hora

	time

Establecer titulo de la ventana cmd

	title [nombre de ventana]

Muestra contenido de archivo texto por ejemplo

	type [nombre de archivo.txt]

Ver la fecha

	date

Cambiar a directorio indicado

	cd

Cambiar a directorio superior

	cd ..

Limpiar pantalla

	cls

Eliminar archivo

	del [archivo]

Color [arg=background][arg=color text] 

	0 = Black       8 = Gray
    1 = Blue        9 = Light Blue
    2 = Green       A = Light Green
    3 = Aqua        B = Light Aqua
    4 = Red         C = Light Red
    5 = Purple      D = Light Purple
    6 = Yellow      E = Light Yellow
    7 = White       F = Bright White

Ver los directorios y archivos en ruta actual

	dir

Ping extendido

	ping -t [ip]

Ping ipv4

	ping -4 [ip]

Ping ipv6

	ping -6 [ip]

Ver la tabla cache

	arp -a

Borrar la tabla cache

	arp -d

Muestra todas las conexiones activas

	netstat -a

Muestra las conexiones en binarios

	netstat -b

Muestra las conexiones sin resolver los nombres

	netstat -n

Consultar nombres de netbios local

	nbtstat -n

Consultar nombres netbios dando ip

	nbtstat -A [ip]

Consultar nombres netbios dando el hostname

	nbtstat -a [hostname]

Ver usuarios del equipo local

	net user

Detener un servicio

	net stop spooler

Iniciar un servicio

	net start spooler

Ver los recursos compartidos con host en red local

	net view \\hostname

Informacion sobre servidores dns 1

	nslookup [nombre de dominio]

Informacion sobre servidores dns 2

	nslookup [ip]

Entrar a cmd como administrador

	run > cmd > ctrl + shift + ENTER

Reiniciar pc

	shutdown /r

Salir de sesión

	shutdown /l

Apagar pc inmediatamente

	shutdown /s /t 0

Abortar apagado

	shutdown /a

Escanea la integridad de los archivos protegidos

	sfc /scannow

Repara errores de archivos en el disco

	chkdsk /f

Localiza sectores erróneos y recuperar informacion

	chkdsk /r

Ver procesos en ejecucion

	tasklist

Terminar procesos por nombre

	taskkill /im [nombre de proceso]

Terminar proceso por pid junto con child process

	taskkill /pid [pid de proceso] /t

Actualizar politicas de grupo

	gpupdate /force

Verificar politicas de grupo

	gpresult /r

Ver puertos conectados (con privilegios)

	netstat -abno

Crear usuarios con contraseñas

	net user /add [nombre de usuario] [contraseña]

Ver el historial

	doskey /history || F7 || F9

Copiar la salida del comando al portapapeles

	[comando] | clip

Ver el estado de los discos

	wmic diskdrive get status, model

Ejecutar la politica de seguridad local

	secpol.msc

Abrir la papelera de reciclaje

	shell:RecycleBinFolder

Filtrar salida de un comando

	comando | find "cadena" /v /c /i
		→ /v salida inversa, las lineas no contienen el string
		→ /c contar el numero de coincidencias
		→ /i ignorar mayusculas o minusculas

Filtrar salida con expresiones regulares

	comando | findstr "[Cc]ejemplo"

Buscar cadena con espacios

	comando | findstr /c: "hello world"

Hacer un ping extendido

	pathping

Añadir hardware

	hdwwiz.exe

Ver la tabla de enrutamiento

	route print

Agregar una ruta

	route add [destination network] mask [subnet mask] [gateway] [cost]

Agregar una ruta persistente

	route -p add [destination network] mask [subnet mask] [gateway] [cost]

Eliminar una ruta

	route delete [destination network]

Ver la tabla arp IPv6

	netsh interface ipv6 show neighbor

Para ver la lista de aplicaciones y poder crear accesos directos

	shell:appsfolder

Abrir el gestor de certificados

	certmgr.msc

Ver todas las opciones de un archivo sin presionar click derecho

	alt + f

Habilitar el gestor de arranque al reinicio de sistema

    bcdedit /set {bootmgr} displaybootmenu [yes|no]
    bcdedit /set {bootmgr} timeout #
    bcdedit /set {bootmgr} timeout 20

Abrir el directorio activo

    dsa.msc

Obtener el nombre de dominio

	wmic computersystem get domain

Configurar si el usuario necesita iniciar sesión con contraseña o no

	netplwiz

Búsqueda LDAP de Microsoft Windows

    ldp.exe

Abrir el panel de Windows Defender

	windowsdefender:

Abrir propiedades del ratón

	main.cpl

Ver las propiedades del sistema remoto

	SystemPropertiesRemote

Activar | Desactivar características de Windows

	optionalfeatures
