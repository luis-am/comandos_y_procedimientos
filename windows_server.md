## Comandos de Windows Server

Ver la version actual de windows server

	DISM /online /Get-CurrentEdition

Hacer el upgrade

	DISM /online /Set-Edition:ServerStandard /ProductKey: **** /	AcceptEULA

Cambiar clave de producto windows

	slmgr -ipk *****-*****...

Activar windows

	slmgr -auto

---

### Editor de politicas locales: gpedit.msc

Configurar actualizaciones automaticas

	administrative templates
	 windows components
	  windows updates 
	   manage end user experience
	    configure automatic update

Mover los registros de evento, habilitar

	configuracion del equipo
	 componentes de windows
	  servicio de registros de eventos
	   aplicacion o instalacion o seguridad 
	    controlar la ubicacion del archivo de registro
	     especificamos la ruta

Ver informe de recursos y diagnosticos

	perfmon /recursos

Editar el archivo de dns

	disco local c
	 windows
	  system 32
	   drivers
	    etc
	     hosts
	     
Activar comunicacion con servidores remotos

	WinRM quickconfig

Habilitar la confianza en el servidor dns

	Set-Item wsman:\localhost\client\TrustedHosts DC2 -concatenate force 	   

Conectar equipos remotamente TrustedHosts

	Enter-PSSession -ComputerName [ip del equipo para acceso remoto -Credential Administrador]

Ver los trustedhost en el sistema

	Get-Item Path WSMan:\localhost\cliente\TrustedHosts

Eliminar trustedhost en el sistema

	Clear-Item -Path WSMan:\localhost\cliente\TrustedHosts

Para sincronizar la hora

	w32tm /resync

Ver en el visor de eventos el equipo en donde se bloqueo una cuenta de usuario

	visor de eventos
	 registros de windows
	  seguridad
	   filtro (id de evento 4740)

Id de evento 4740

	bloqueo de cuenta

Ver caracteristicas opcionales del servidor

	Get-ADOptionalFeature -Filter *

Habilitar caracteristica opcional

	Enable-ADOptionalFeature 'Privileged Access Management Feature' -Scope ForestOrConfigurationSet -Target luis.com

Dar un tiempo de vida a un usuario dentro de un grupo

	Add-ADGroupMember -Identity 'grupo2' -Members 'usuario1' -MemberTimeToLive (New-TimeSpan -Minutes 1)

Ver miembros de grupo

	Get-ADGroupMember 'grupo2'

Unir de manera offline al dominio (en servidor)

	djoin.exe /provision /domain luis.com /machine pc04 /savefile c:/pc04domain

Unir de manera offline al dominio (en cliente)

	djoin.exe /requestODJ /LoadFile C:\pc04domain /WindowsPath c:\Windows\ /LocalOS

Redireccionar equipos en el dominio

	propiedades de computadora
	 extensiones
	  editor de atributos
	   distinguishedname (copiar valor)
	    -- en powershell --
	      redircmp "OU=EQUIPOS,OU=LABORATORIO,DC=luis,DC=com"

Modificar el tombstone lifetime

	herramientas
	 editor adsi
	  click derecho en editor adsi > conectar a
	   seleccione un contexto de nomenclatura conocido
	    configuracion
	     aceptar
	configuracion servidor01.luis.com
	 CN=Configuration,DC=luis,DC=com
	  CN=Services
	   CN=Windows NT
	    CN=Directory Service
	     propiedades
	      atributo tombstoneLifetime
	       valor numero de dias

Hacer consultas rpc

	wmic /node:pc01 computersystem get username

---
---

Ver el estado de la replicacion entre dos controladores de dominio

	repadmin /showrepl

> Hay dos tipos de replicacion: de objetos y sistema de archivos

> FSR replica todo, DFS-R replica los cambios

Ver el estado de replicacion

	dfsrmig /getglobalstate

Ver quien es el controlador de dominio principal

	netdom query fsmo

---

### Conceptos de Windows Server

**Bosque**: Es el mayor contenedor logico y abarca a todos los dominios. debe haber relacion de confianza entre dominios.

**Arbol**: Coleccion de dominios que abarca varios dominios que depende de una raiz comun

**Dominio**: Coleccion de objetos dentro del directorio activo

**Unidad organizativa**: Contenedor de objetos formados jerarquicamente, simplifica la delegacion de objetos

**Objeto**: componente que forma parte del directorio

**kerberos**: Protocolo de autenticacion de redes de ordenadores, se basa en criptografia de clave simetrica, autenticacion y seguridad cliente servidor

**LDAP**: Protocolo que construyen la estructura jerarquica

---

### LAPS (local administrator password solution) instalacion y configuracion

Descargar laps desde la pagina oficial de microsoft e instalar todos los componentes del paquete en el SERVIDOR

Para hacer un deploy de software en las maquinas clientes creamos una carpeta en el disco c del servidor (ejemplo nombre LAPS)

Establecemos la carpeta como oculta y lo compartimos con el grupo equipos del dominio, al igual que darle permiso en la pestaña de seguridad

Colocamos el ejecutable de LAPS en la carpeta creada en el servidor

Asignamos la unidad organizativa en donde se encuentran los equipos (ejemplo UO_LAPS)

En politicas de grupo creamos una politica en UO_LAPS

Editamos la politica

	computer configuration
	 policies
	  software settings
	   software installation
	    click derecho > new package
	     file name: \\SERVIDOR\LAPS$\LAPSx64.msi

Fixing an identical sid while joining an active directory domain

	C:\Windows\System32\Sysprep\sysprep.exe
	check global

- Eliminar un usuario

	Remove-ADUser -Identity USERNAME

- Desbloquear una cuenta

	Unlock-ADAccount -Identity USERNAME

- Reset user password

	Set-ADAccountPassword -Identity USERNAME -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "NewP@ssw0rdReset!" -Force)

- Force password change

	Set-ADUser -Identity amasters -ChangePasswordAtLogon $true

- Crear una nueva unidad organizativa

	New-ADOrganizationalUnit -Name "Security Analysts" -Path "OU=IT,OU=HQ-NYC,OU=Employees,OU=CORP,DC=INLANEFREIGHT,DC=LOCAL"

- Crear una nueva GPO aplicado a una unidad organizativa

	New-ADGroup -Name "Security Analysts" -SamAccountName analysts -GroupCategory Security -GroupScope Global -DisplayName "Security Analysts" -Path "OU=Security Analysts,OU=IT,OU=HQ-NYC,OU=Employees,OU=Corp,DC=INLANEFREIGHT,DC=LOCAL" -Description "Members of this group are Security Analysts under the IT OU"

- Agregar un usuario a un grupo

	Add-ADGroupMember -Identity analysts -Members ACepheus,OStarchaser,ACallisto

- Duplicar una gpo

	Copy-GPO -SourceName "Logon Banner" -TargetName "Security Analysts Control"

- Aplicar una gpo a una UO

	New-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes
