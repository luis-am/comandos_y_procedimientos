## Comandos

### Conectarse a un servidor

	xfreerdp /sec:[PROTOCOL] /v:[IP] /u:[USERNAME] /p:[PASSWORD]
	xfreerdp /v:192.168.10.122 /u:usertest /p:P@ssw0rd
	xfreerdp /sec:tls /v:192.168.10.122 /u:testuser /p:P@ssw0rd
	xfreerdp /sec:rdp /v:192.168.10.122 /u:testuser /p:P@ssw0rd
	xfreerdp /sec:rdp /v:192.168.122.50 /d:luisayala /u:luisadmin /p:P@ssw0rd /dynamic-resolution

	v: server
	d: domain
	u: user
	p: password
