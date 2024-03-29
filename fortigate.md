## Comandos de Fortigate

Ver interfaces

	get system interface

Modo interface

	config system interface
		show
		get
		edit port[#]
			set ip x.x.x.x/X
			set allowaccess [ping, http, etc]
			unset allowaccess
			end

Hacer un ping

	execute ping x.x.x.x

Reiniciar

	execute reboot

Estado de fábrica

	execute factoryreset

Grepeo

	show | grep -fi port1 i viene de insensitive
	show full-configuration
	next (es como cd en linux)
	abort (no guarda la configuracion)
	end (guarda la configuracion)

Config system dhcp server

	config firewall address
	config firewall addrgrp
	edit equipos\site\1
		set member []
		append member []
		clear member
		unselect member

---

### Apagado, reiniciado de sistema

Apagar sistema

	execute shutdown

Reiniciar sistema

	execute reboot

---

### Routing - reverse path forwarding

Habilitar metodos rpf, disable = loose, enable = strict

	conf system settings
	set strict-src-check [ disable | enable ]
	end

Deshabilitar rpf checking

	config system settings
	set asymroute enable
	end

Deshabilitar rpf checking a nivel de interface

	config system interface
	edit <interface>
	set src-check [ enable | disable ]
	end

---

## Routing - ecmp
	
Establecer el metodo ecmp

	config system settings
	set v4-ecmp-mode [ source-ip-based | usage-based | source-ip-based | weight-based ]
	end

Establecer weight ecmp ya sea por interface o ruta

	config system interface
	set <interface name>
	set weight <0 to 255>
	end

	config router static
	edit <id>
	set weight <0 to 255>
	end

Establecer umbrales spillover por interface

	config system interface
	edit <interface name> 
	set spillover-thresold <0 to 16776000>
	end

---

### Routing - link health monitor configuration

Configurar health link monitor

	config system link-monitor
	edit <name>
	set srcinf <interface>
	set server <server ip>
	set gateway-ip <gateway ip>
	set protocol [ ping | tcp-echo | udp-echo | twamp | http]
	set update-static-route [ enable | disable ]
	next
	end

---

### Routing - diagnostics
	
Ver las rutas activas

	get router info routing-table all

Ver todas las rutas en general

	get router info routing-table database

Ver las policy routes y isdb routes

	diagnose firewall proute list

Captura de paquetes

	diagnose sniffer packet <interface> '<filter>' <verbosity > <count> <timestamp> <frame
	ex: diagnose sniffer packet any 'icmp' 4
	ex: diagnose sniffer packet any 'port 443' 4
	ex: diagnose sniffer packet any 'host 192.168.1.254 and icmp' 3

---

### SD-WAN local breakout

Establecer metodo balanceo sd-wan

	config system sdwan
		set load-balance-mode [load balance mode]
	end

SLA cli configuracion sd-wan

	config system sdwan
	set status enable
	config health-check
	edit <name>
	set protocol [ ping | tcp-echo | udp-echo | http | dns | twamp | tcp-connect | ftp]
	set server <server ip>
	set detect-mode [ active | passive | prefer-passive]
	set threshold-warning-packetloss <percentage>
	set threshold-alert-packetloss <percentage>
	set threshold-warning-latency <ms>
	set threshold-alert-latency <ms>
	set threshold-warning-jitter <ms>
	set threshold-alert-jitter <ms>
	set probe-packet enable
	set ha-priority <1-50>

	config system sdwan
	set status enable
	config health-check
	edit <name>
	set interval <500-3600>
	set failtime <1-3600>
	set recoverytime <1-3600>
	set member <0, 1, 2, ...>
	set probe-timeout <500-5000 msec>
	config sla
	edit <id>
	set link-cost-factor [latency | jitter | packet-loss]
	set latency-threshold <integer> (0 - 10000000)
	set jitter-threshold <integer> (0 - 10000000)
	set packetloss-threshold <integer> (0 - 100)
	next

---

Layer 2 switching

Subdividir una vdom en multiples dominios de broadcast

	config system interface
		edit <interface_name>
			set forward-domain <domain_ID>
	end 

Ver tabla mac en modo transparente

	diagnose netlink brctl name host <vdom name>.b

---

### VDOMS

Habilitar vdoms

	config system global
		set vdom-mode no-vdom/split-vdom/multi-vdom
	end

Establecer modo de operacion per-vdom

	config vdom
	edit <vdom>
		config system settings
			set opmode [nat | transparent]
		end

Habilitar prompt de confirmacion vdom

	config system global
		set edit-vdom-prompt [ enable | disable]
	end

Accesando a global settings

	config global

Accesando a per-vdom settings

	config vdom
		edit <vdom-name>

Ejecutar comandos globales o per-vdom desde cualquier contexto

	[global | vdom-name] sudo [global | vdom-name] [diagnose | execute | show | get]

Realizar sniffer trace

	diagnose sniffer packet <interface_name> <’filter’> <verbose> <count>

Realizar un packet flow trace

	diagnose debug enable
	diagnose debug flow filter addr <PC1>
	diagnose debug flow trace start 100

---

### Ipsec protocol

Cambiar por defecto los puertos de ike e ike nat

	config system settings
		set ike-port <integer>
		set ike-natt-port <integer>
	end

---

### High availability
	
Forzar un failover

	diagnose sys ha reset-uptime

Verificar las diferencias uptime ha

	diagnose sys ha dump-by vcluster

Habilitar 'override enable' en ha

	config system ha
		set override enable
	end

Habilitar tabla de sincronizacion para mayoria de sesiones tcp e ipsec vpn

	config system ha
		set session-pickup enable
	end

Habilitar sincronización de sesiones udp e icmp

	config system ha
		set session-pickup enable
		set session-pickup-connectionless enable
	end

Habilitar sincronizacion de sesiones multicast

	config system ha
		set multicast-ttl <5 – 3600 sec>
	end

Ver el status de ha

	diagnose sys ha status

Verificando la sincronizacion de configuracion

	diagnose sys ha checksum

Entrar a la cli del secondary fortigate desde primary fortigate

	execute ha manage [cluster_id] [Admin_Username]
	execute ha manage 0 admin

Para listar los numeros de indice de cada fortigate

	execute ha manage ?

Forzar failover en el primary fortigate

	execute ha failover set [cluster_id] 
	execute ha failover set 1

Ver el status del failover

	execute ha failover status

Detener el failover status

	execute ha failover unset 1

Ver el system status luego del failover deshabilitado

	get system ha status

Configurar una interface de gestion ha in-band

	config system interface
		edit <port name>
		set management-ip <IP address and subnet mask>
	end

Ver el numero de sesiones en fortigate

	get system session status

Comandos de diagnostico	 para ver failover en tiempo real

	diagnose debug enable
	diagnose debug application hatalk 0
	diagnose debug application hatalk 255

Detener el debug de ha failover

	diagnose debug application hatalk 0

Configurar ha via cli

	config system ha
		set group-name Training
		set mode a-a
		set password Fortinet
		set hbdev port2 0
		set session-pickup enable
		set override disable
		set priority 100
	end

---

### Diagnostics

Ver informacion del sistema

	get system status

Ver informacion de una interface

	get hardware nic <interface_name>

Ver tabla arp

	get system arp

Opciones de troubleshooting en la capa de red

	execute ping-options

Comando multi-step 'debug flow'

	diagnose debug flow filter <filter>
	diagnose debug enable
	diagnose debug flow trace start <xxx> Repeat number
	diagnose debug flow trace stop

Que tan alto es el uso del cpu

	get system performance status
	diagnose sys top 1
	diagnose sys top
		ordenar cpu: shift + p
		ordenar memoria: shift + m

Habilitar 'memory conserver mode' (default, se puede cambiar los valores)

	config system global
		set memory-use-threshold-green 82%
		set memory-use-threshold-red 88%
		set memory-use-threshold-extreme 95%
	end

Configurar inspecccion de paquetes por el ips en modo 'conserve'

	config ips global
		set fail-open [enable | disable]
	end

Para trafico que requiera inspeccion basado en proxy

	config system global
		set av-failopen [off | pass | one-shot]
	end

Diagnostico 'conserver mode' memoria del sistema

	diagnose hardware sysinfo conserve

Configurar como las sesiones son impactadas por scan error utm

	config system global
		set av-failopen-session [enable | disable]
	end

Fortios hardware tests command

	diagnose hardware test suite all

Verificar los crash logs

	diagnose debug crashlog history
	diagnose debug crashlog read

---

### Firewall policies

Deshabilitar actualizaciones isdb

	config system fortiguard
		set update-ffdb [enable | disable]
		next
	end

Configurar el nombre de la politica via cli

	config firewall policy
		edit 1
			set name “Training"
			set uuid 2204966e-47f7-51..

Denegar la politica

	config system setting
		set ses-denied-traffic <disable | enable>
	end
	config system global
		set block-session-timer <1-300>
	end

---

### NAT

(Modificar el deny policy) enable match-vip in deny policy

	config firewall policy
		edit <policy ID for deny>
		set match-vip enable
	end

(Modificar el deny policy) set the destination address as vip object

	config firewall policy
		edit <policy ID for deny>
		set dstaddr “VIP object”
	end

Habilitar o deshabilitar central nat

	config system settings
		set central-nat {enable|disable}
	end

Excluir un vip cuando central nat esta habilitado

	config firewall vip
		edit "name_of_the_VIP"
		set status disable
		next
	end

Mostrar sessions helpers configurados

	show system session-helper

Configurar la sesion ttl por defecto

	config system session-ttl
		set default 3600
	end

Especificando los temporizadores de estados

	config system global
		set tcp-halfclose-timer 120
		set tcp-halfopen-timer 10
		set tcp-timewait-timer 1
		set udp-idle-timer 180
	end

Diagnosticar sesiones de firewall

	diagnose sys session

Limpiar previos filtros de diagnostico de firewall

	diagnose sys session filter clear

Listar todas las entradas que hacen match en el filtro configurado

	diagnose sys session list

Purgar todas las entradas que hacen match con el filtro configurado

	diagnose sys session clear

Ejemplo de ver la tabla de sesion tcp

	diagnose sys session filter dst 10.200.1.254
	diag sys session filter dport 80
	diag sys session list

Ver si se ha producido port exhaustion (importante el valor de clash)	

	diagnose system session stat

Listar todos los pools ip configurados

	diagnose firewall ippool-all list

Para ver los states de los pools

	diagnose firewall ippool-all stats <Optional IP Pool name>

---

### Antivirus

Habilitar el scan machine learning

	config antivirus settings
		set machine-learning-detection {enable| monitor | disable}
	end

Habilitar Fortigate para recibir signature database desde FortiSandBox

    set gui-fortigate-cloud-sandbox enable

Verificar las versiones de firmas de antivirus

	diagnose autoupdate status
	diagnose autoupdate versions

Seleccionar el database de firmas de antivirus (cli only)

	config antivirus settings
		set use-extreme-db {enable | disable}
	end

Configurar politicas de firewall proxy-based y flow-based, configurar opciones de protocolos

	config firewall profile-protocol-options
		edit <profile_name>
	config <protocol_name>

Habilitar log para archivos oversize

	config firewall profile-protocol-options
		edit <profile_name>
		set oversize-log {enable|disable}
	end

Habilitar aceleracion nturbo

	config ips global
		set np-accel-mode {none | basic}
	end

Habilitar av scan offloading al cp procesador

	config ips global
		set cp-accel-mode {none | basic | advanced}
	end

Forzar chequeo de nuevas actualizaciones de antivirus

	execute update-av

Algunos comandos utiles de antivirus

	get system performance status
	diagnose antivirus database-info
	diagnose autoupdate versions
	diagnose antivirus test "get scantime"
	execute update-av

Ver las Ip de las interfaces físicas

    get system interface physical

# Ver el healt-status de sd-wan

    diagnose sys sdwan health-check

# Fórmula para medir la calidad del enlace

    Link Quality = (a*latency)+(b*jitter)+(c*packet loss)+(d/bandwidth)
    
# 
