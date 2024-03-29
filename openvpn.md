# Configuración OpenVPN
#### Configuración de OpenVPN3 para Linux

# Importar un archivo de configuración
	openvpn3 config-import --config [NAME]

# Importar un archivo de configuración y hacerlo persistente luego de cada reinicio
	openvpn3 config-import --config [NAME] --persistent

# Iniciar una sesión con una config ya importada
	openvpn3 session-start --config [NAME]

# Ver la lista de configs importados
	openvpn3 configs-list

# Listar todas las sesiones activas
	openvpn3 sessions-list

# Desconectarse de una sesión activa
	openvpn3 session-manage --disconnect --config [NAME]

# Borrar una configuración importada (esta es la ruta que muestra cuando ejecutamos el comando openvpn3 configs-list)
	openvpn3 config-remove --path /net/openvpn/v3/configuration/d8f4d71bxbeb3x4e3fx9056xe56111bd3f36

# Eliminar una sesión teniendo como parámetro --path
	openvpn3 session-manage --path /net/openvpn/v3/configuration/d8f4d71bxbeb3x4e3fx9056xe56111bd3f36
