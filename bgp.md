# BGP COMANDOS

## Configuración básica para armar la vecindad y advertir las redes.

	configure terminal
	router bgp [AS]
	neighbour [IP] remote-as [AS]
	network [NETWORK] mask [MASK]
	end

## Sumarizar rutas
llaCam
	configure terminal
	router bgp [AS]
	aggregate-address [SUMMARIZED NETWORK] [MASK] summary-only

## Comandos de verificación
    
    show ip bgp neighbour
    show bgp
    show ip bgp
    show ip bgp summary

## Multi-hop

    configure terminal
    router bgp [AS]
    neighbour [IP] remote-as [AS]
    neighbour [IP] ebgp-multihop 2

## Cambiar de formato AS
    
    router bgp [AS]
    bgp asnotation dot

## Cambiar por defecto la versión de IPv4  IPv6
    
    router bgp [AS]
    no bgp default ipv4 unicast

## Cambiar a la familia ya sea IPv4 o IPv6

    router bgp
    no bgp default ipv4 unicast
    address-family ipv4 unicast
    neighbour x.x.x.x activate
