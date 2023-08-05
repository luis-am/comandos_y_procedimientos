### Generación de llaves para conexión a Github.

---

Generar un par de llaves de tipo de sistema de cifrado'ed25519', la opción '-t' significa tipo y '-C' es el comentario.
	
	ssh-keygen -t ed25519 -C "Conexion hacia GitHub."

Verificar el checksum de llave publica, donde '-l' es para mostrar la longitud de la clave y el fingerprint. La opción 'f' es para seleccionar el archivo de clave que se usará para la operación.

	ssh-keygen -l -f ~/.ssh/id_ed25519_github.pub

Iniciar el agente ssh en el background.

	eval "$(ssh-agent -s)"

Añadir la llave privada al agente.

	ssh-add ~/.ssh/id_ed25519_github

Verificar el fingerprint de la llave publica en el agente, donde '-l' es para listar las claves, y '-E' para especificar el algoritmo.

	ssh-add -l -E sha256

Copiar la llave publica de Github.

	cat ~/.ssh/id_ed25519_github.pub | xclip -selection clipboard

Probar conectividad con GitHub, donde '-T' significa deshabilitar la pseudoterminal.
	
	ssh -T git@github.com

> Output: Hi luis-am! You've successfully authenticated, but GitHub does not provide shell access. 
