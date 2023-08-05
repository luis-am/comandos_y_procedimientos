# usar como ejemplo
	SSH server: 10.10.10.2
	SSH client: 10.10.10.1

# conectarse via ssh al server
	input: ssh username@10.10.10.2

# salir de la sesion
	input: ctrl + d

# configurar el archivo config en el cliente
	input: ~/.ssh/config
		type: Host server (puede ser cualquier nombre que identifique al server al que queremos conectarnos)
						Hostname 10.10.10.2
						Port 22
						User username

# generate key-pair, por defecto utiliza el algoritmo RSA
		input: ssh-keygen
		type: passphrase
# se generaran dos archivos uno id_rsa (privada) y el otro id_rsa.pub (publica)

# copy public key to the server
		input: ssh-copy-id -i ~/.ssh/id_rsa.pub username@10.10.10.2
			-i: input

# generar una key con el numero de bits deseados (por defecto es 2048)
		input: ssh-keygen -b 4096 

# para cambiar o eliminar el passphrase
		input: ssh-keygen -p

# para encontrar el fingerprint de la private publica ---> ssh-keygen -l [-v] [-E fingerprint_hash] [-f input_keyfile]
		input: ssh-keygen -l -f [path]
			-l: fingerprint
			-f: file

# generar una key mas segura
		input: ssh-keygen -t ed25519 -C "acme"
			-t: type
			-C: commentary

# copy public key to a server
		input: ssh-copy-id -i ~/.ssh/acme_id_ed255519.pub username@10.10.10.2

# iniciar SSH agent
		input: eval "$(ssh-agent)"

#  ver el ssh agent ejecutandose
		input: ps aux | grep ssh-agent

#  agregar la key privada al agente
	input: ssh-add ~/.ssh/acme_id_ed255519

# ejecutar un comando en un servidor remoto
		input: ssh username@10.10.10.2 [command]

# logging a un server con un diferente puerto
		input: ssh -p [port] username@10.10.10.2

# logging a un server con solo llaves publicas
		input: ssh -i [public_key] username@10.10.10.2

# configurando de manera segura el servidor
		path: /etc/ssh/sshd_config
			(deshabilita la autenticacion por passwords, en este caso solo usan las keys)
				line: PasswordAuthentication no
			(limitar el acceso a usuarios)
				line: AllowUsers [usuario1] [usuario2]
			(limitar el acceso a usuarios)
				line:AllowGroups [grupo]
			(disable root login)
				line: PermitRootLogin no
		reiniciar el servicio para efectuar cambios

# crear un grupo sin home directory
		input: sudo groupadd -r [sshMembers]

# agregar usuarios al grupo SSH
		input: usermod -a -G [sshMembers] [user1]

# configurando el lado del cliente SSH
		path: ~/.ssh/config
			mandar paquetes cada cierto tiempo para evitar el cierre de sesion (timeout)
				Host *
					ServerAliveInterval 120
					
# ejemplo de config file
		Host server1
     		HostName x.x.x.x
     		User [username]
     		Port [#port]
     		IdentityFile /home/luisam/.ssh/[private_key]


# agregar la llava privada al agente ssh
	ssh-add [PRIVATE_KEY_LOCATION]

# remover la llave privada al agente ssh
	ssh-add -d [PRIVATE_KEY_LOCATION] 

# remover todas las llaves privadas del agente
	ssh-add -D

# comando usando ssh-pass

	for user in ansible root; do   for os in ubuntu centos;   do     for instance in 1 2 3;     do       sshpass -f password.txt ssh-copy-id -o StrictHostKeyChecking=no ${user}@${os}${instance};     done;   done; done
