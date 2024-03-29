## Comandos de Powershell

Get-Alias dir

Vaciar el portapapeles

	Clear-RecycleBin

Listing the drives

	Get-PSdrive
	Get-PSdrive -PSProvider FileSystem

Listing files

	Get-ChildItem

Changing the location

	Set-Location [location]

Create a new item

	New-Item -ItemType Directory -Path [locationPath] -Name [nameFolder]			// para crear un folder
	New-Item -ItemType File -Path [locationPath] -Name [nameFolder] -Value "[text]"			// para crear un archivo
	Set-Content -Path [locationPath] -Value "[nuevoTexto]"			// cambiar el contenido de un archivo de texto

Ver informacion de un archivo

	Get-Item [locationPath] 			// ver características de un archivo
	Get-Get-Content [locationPath] 			// ver el contenido de un archivo

Renombrar un archivo

	Rename-Item -Path [locationPath] -NewName [newName]

Copiar y mover un archivo 

	Copy-Item -Path [name] -Destination [locationPathNewName]
	Move-Item -Path [name] -Destination [locationPathNewName]

Eliminar un archivo

	Remove-Item -Path [locationPath]

Ver los comandos disponibles

	Get-Command -CommandType [Cmdlet] 			// ver por tipo de comando
	Get-Command *[item] 			// ver por nombre

Ver la ayuda de un comando

	Get-Help [command]
	Get-Help [command] -Example

Ver los procesos y servicios

	Get-Process
	Get-Service

Detener un proceso

	Stop-Process -Name [nameProcess]
	Get-Process -Name [nameProcess] 			// para ver las instancias de un proceso antes de detener
	Stop-Process -Id [idNumber] -Confirm -PassThru 			// kill procesos por el número de Id

Ver los drivers online del sistema

	Get-WindowsDriver -Online -all

Ver información de IP

	Get-NetIPAddress
	Get-NetIPAddress -InterfaceIndex [indexNumber]
	Get-NetIPConfiguration -InterfaceIndex [indexNumber]
	Get-NetAdapter -InterfaceIndex 10			// ver informacion breve de adaptadores
	New-NetIPAddress -InterfaceIndex [indexNumber] -IPAddress [IP] -PrefixLength [prefix] -DefaultGateway [IP]
	Set-DnsClientServerAddress -InterfaceIndex [indexNumber] -ServerAddresses "[IP1] , [IP2]"

// MOSTRAR LA CONFIGURACIÓN ACTUAL:
	
	netsh interface ipv4 show config

// ESTABLECER LA IP ESTÁTICA, MÁSCARA DE SUBRED Y EL GATEWAY

	netsh interface ipv4 set address name="YOUR INTERFACE NAME" static IP_ADDRESS SUBNET_MASK GATEWAY

// ESTABLECER IP DINÁMICA	

	netsh interface ipv4 set address name="YOUR INTERFACE NAME" source=dhcp

// ESTABLECER EL DNS

	netsh interface ipv4 set dns name="YOUR INTERFACE NAME" static DNS_SERVER

// ESTABLECER EL SEGUNDO DNS

	netsh interface ipv4 set dns name="YOUR INTERFACE NAME" static DNS_SERVER index=2

// CAMBIAR EL HOSTNAME

	Rename-Computer -NewName "HOSTNAME"

// OBTENER EL HASH DE UN FILE

	Get-FileHash -Algorithm md5 test.txt

// APAGAR O REINICIAR LA COMPUTADORA

	shutdown /s /t 0
	shutdown /r /t 0

// VER LA INFORMACIÓN DE USO DE ALMACENAMIENTO

	get-psdrive


##### Common Verbs GET, SET, NEW, ADD, REMOVE

// VER TODOS LOS COMANDOS DISPONIBLES A TRAVÉS DE MODULOS

	get-command -module [MODULE]

// VER AYUDA DE LOS COMANDOS

	get-help [*NOUN*]

// ALIAS CONOCIDOS

	cgi - get-childitem
	mkdir - new-item
	cd - set-location

// OBTENER LA LISTA DE ARCHIVOS DE MANERA ORDENADA

	ls | sort LastAccessTime

// LISTAR DE MANERA RECURSIVA

	dir -recurse

// net use z: \\server\c$

// Ver los procesos

	get-process

// Botar la salida de un comando a un archivo

	ipconfig /all > file.txt | notepad file.txt
	ipconfig /all >> file.txt | notepad file.txt

// VER EL CONTENIDO DE UN ARCHIVO

	cat [FILE]
	get-content [FILE]

// VER LA INFORMACION DE UN USUARIO EN EL DIRECTORIO ACTIVO

	get-aduser -identity '[USERNAME]'

// OBTENER LA LISTA DE ADAPTADORES DEL SISTEMA
	
	get-netadapter

// VER LA DIRECCIÓN IP DE LOS ADAPTADORES

	get-netipaddress

// ESTABLECER NUEVA DIRECCIÓN IP

	New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress "192.168.1.100" -PrefixLength 24 -DefaultGateway "192.168.1.1"


