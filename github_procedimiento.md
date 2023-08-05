Generar un par de llaves de tipo 'ed25519', la opción '-t' significa tipo y '-C' es el comentario.
	
	input: ssh-keygen -t ed25519 -C "Conexion hacia GitHub."

Verificar el checksum de llave publica

	input: ssh-keygen -l -f ~/.ssh/id_ed25519_github.pub

Iniciar el agente ssh en el background

	input: eval "$(ssh-agent -s)"

Añadir la llave privada al agente

	input: ssh-add ~/.ssh/id_ed25519_github

Verificar el fingerprint de la llave publica en el agente

	input: ssh-add -l -E sha256

Copiar la llave publica en GitHub

	input: cat ~/.ssh/id_ed25519_github.pub | xclip -selection clipboard

Probar conectividad con GitHub
	
	input: ssh -T git@github.com
	output: Hi luis-am! You've successfully authenticated, but GitHub does not provide shell access. 
	-T: deshabilitar pseudoterminal

