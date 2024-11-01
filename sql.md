# Iniciar sesión con el usuario

	- mysql -u root -p

# Mostrar las bases de datos

	- show databases;

# Crear un nuevo usuario

	- create user 'luisam'@'10.0.0.10' identified by 'password';

# Brindar permisos a usuario nuevo

	- grant all on *.* to 'luisam'@'10.0.0.10' with grant option;

# Depurar los privilegios

	- flush privileges;

# Eliminar un usuario

	- drop user 'luisam'@'10.0.0.10';

# Ingresar desde otra línea de comandos

	- mysql -uuser -hhostname -PPORT -ppassword

# Ver los usuarios

	- select user from mysql.user;

##############################################################

# Cambiar la contraseña del usuario postgres

	- sudo -u postgres psql postgres
	postgres=# \password postgres
