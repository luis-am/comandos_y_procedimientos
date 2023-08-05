// ver el tamaño que ocupa un directorio
		input: du -sh /directorio

// crear carpetas consecutivas
		input: mkdir -p /directorio1/directorio2/directorio3

// comando para comprimir
		input: zip -r directorio1.zip /directorio1

// crear usuario con su grupo primario
		input: useradd -g grupo1 usuario1

// cambiar de nombre al equipo
		input: hostnamectl set-hostname	