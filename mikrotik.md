## Comandos de Mikrotik

Resumen de la configuracion 

	export

Setear la hora peruana 

	system clock set time-zone-name=Etc/GMT+5

Asignar nombre al equipo 

	sys iden set n=[abc]

Ver la hora 

	system clock print

Setear contraseña 

	user set admin password=[abc]

Añadir usuario con contraseña 

	user add name=[usuario] group=full password=[password]

Añadir a grupo con politicas 

	user group add name=[grupo] policy=read,telnet,winbox,local

Print usuarios, habilitar, deshabilitar 

	user print
	user enable [number]
	user disable [number]

Asignar direccion ip a una interface 

	ip address add address=x.x.x.x/x interface=[ether#] comment=[abc]

Crear una interface loopback 

	/interface bridge add name=[abc] comment:[abc]

Habilitar una interface 

	interface enable [#]

Habilitar una interface 

	interface disable [#]

Habilitar ip address de interface

	ip add enable [#]

Deshabilitar ip address de interface

	ip add disable [#]

Ruta predeterminada 

	/ip route add gateway=x.x.x.x

Ruta estatica 

	/ip route add dst-address=x.x.x.x/x gateway=x.x.x.x

Seter dns server 

	ip dns set servers=x.x.x.x

Salida a internet nat 

	ip fire nat add chain=srcnat out-interface=[abc] action=masquerade

Volver a estado de fabrica 

	sys reset no-defatul=yes

Hacer ping o traceroute 

	tool ping x.x.x.x
	tool traceroute x.x.x.x

Crear un pool para dhcp-server 

	ip pool add name=[abc] ranges=x.x.x.x-x.x.x.x

Crear el servidor dhcp 

	ip dhcp-server add name=[abc] interface=ether# address-pool=[abc]

Crear la red 

	ip dhcp-server network add address=x.x.x.x/x gateway=x.x.x.x dns-server=x.x.x.x

Convertir una interface en cliente-dchp 

	ip dhcp-client add interface=ether# add-default-route=yes

Enviar los logs a un servidor log 

	sys logg action add name=[abc] remote=x.x.x.x remote-port=514 target=remote

Ver los archivos  exportados 

	file print brief

Exportar un archivo 

	export file=[abc]

---

### Routing OSPF 

Crear instancia 

	int bri add name=loopback0
	ip add add add=x.x.x.x int=loopback0	
	routing id add name=rid id=10.1.1.1
	routing ospf instance add name=instancia1 version=2 vrf=main originate-default= always router-id=rid

Crear area 

	routing ospf area add name=backbone instance=instancia1 area-id=0.0.0.0

Crear interface-template 

	routing ospf interface-template add interfaces=ether1 area=backbone type=ptp auth=md5 auth-key=cisco
	routing ospf interface-template/add interfaces=ether2 area=backbone type=broadcast auth=md5 auth-key=cisco
	routing ospf interface-template add interfaces=ether3 area=backbone type=broadcast passive
