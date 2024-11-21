## Comandos de smbclient

- Listar todos los shares disponibles

    smbclient -N -L \\\\[IP ADDRESS]
    smbclient -N -L \\\\[192.168.122.1]

    -N: suprimir el prompt de contraseña
    -L: listar los shares disponibles
* importa el orden, primero la -N, luego lo demás.

- Conectarse a un share como 'guest user'

    smbclient \\\\[IP ADDRESS]\\users
    smbclient \\\\192.168.122.1\\users

- Conectarse a un share especificando usuario

    smbclient -U [USER] \\\\[IP ADDRESS]\\users
    smbclient -U user1 \\\\192.168.122.1\\users

- Leer un archivo estando dentro del smb-share

    more [FILE]
    more file.txt
