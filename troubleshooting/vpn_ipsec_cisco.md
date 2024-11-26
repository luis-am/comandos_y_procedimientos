Configuración Básica
	1. Direccionamiento de la topología
	2. Crear rutas estáticas predeterminadas

Configuración IPsec
1. Configurar fase 1 ISAKMP
		crypto isakmp policy 1
		encryption aes 256
		hash sha256
		authentication pre-share
		group 14
	crypto isakmp key cisco address 200.200.200.1

2. Identificar el tráfico interesante
	ip access-list extended VPN-IPSEC
	permit ip 192.168.50.0 0.0.0.255 172.16.10.0 0.0.0.255

3. Configurar fase 2 ISAKMP
	crypto ipsec transform-set LUIS esp-aes esp-sha512-hmac

4. Crear el crypto-map
	crypto map SAR 10 ipsec-isakmp
	set peer 200.200.200.1
	set transform-set LUIS
	match address VPN-IPSEC

5. Aplicar el crypto map a interface wan
	crypto map SAR
	
6. Generar el tráfico