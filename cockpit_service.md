### Servicio de Cockpit

---

Allow external connections to port 9090 through the firewall.

	firewall-cmd --add-port=9090/tcp
	firewall-cmd --permanent --add-port=9090/tcp

Install the cockpit packages.

	sudo yum install cockpit

Enable and start the cockpit.socket service.

	sudo systemctl enable cockpit.socket
	sudo systemctl start cockpit.socket

Ruta de del archivo de configuracion de cockpit.

	/etc/cockpit/cockpit.conf

Dentro del archivo se ve esto.

	[basic]
	LoginTitle = RHEL
	ClientCertAuthentication = false
	Banner = "Welcome Luis!"

Entrar por la web.

	https://x.x.x.x:9090/
