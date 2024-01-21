# Quién soy?

	whoami

# Ver los grupos al cual pertenezco
	
	id

# Ver la ruta absoluta de un binario, también se puede usar el siguiente comando para visualizar la ruta absouluta
	
	- which cat
	- command -v cat

# Ver el código de estado, donde 0: exitoso 
	
	- $?

# Mandar el stdout y stderr al /dev/null.

	- command &> /dev/null

# Abrir wireshark y no mostrar nada en la consola

	- wireshark &> /dev/null &
	- wireshark &> /dev/null & disown

# Establecer un descriptor a un archivo

	- exec 3<> file
	- whoami >&3
	- cat file

# Cerrar el descriptor de archivo
	
	- exec 3>&-

# Copiar un descriptor de archivo a otro

	- exec 8>&5

# Copiar un descriptor de archivo a otro y cerrar el anterior a la vez

	- exec 8>&5-

# Cambiar de grupo

    - chgrp newgroup file

# Asignar permisos en una sola línea
    
    - chmod u+x,g-rx,o+w,o-x file|folder

# Crear un usuario

    - useradd pepe -s /bin/bash -d /home/pepe

# Crear un nuevo grupo

    - groupadd Alumnos

# Eliminar un usuario junto con su home directory

    - sudo userdel -r [USER]

# Control de atributos de ficheros en Linux - Chattr y Lsattr

    - lsattr: listar atributos
    - chattr: cambiar atributos

# Cambiar el atributo a inmutable a un archivo

    - chattr +i [FILE]

# Aplicar doble comando al inicial

    - which python3.11 | xargs ls -l

# Permisos especiales

    - SUID: 4000
    - GUID: 2000

# Ver las capabilities de Linux, es una buena forma de elevar nuestros priviligios

    - getcap / -r 2>/dev/null

# El userID de root es "0"

# Directorio bin:

    Se encuentran los binarios para ejecutar a nivel de usuario

# Directorio sbin:

    Binarios para tareas propias del sistema operativo y el usuario root.

# Directorio boot:

    Se encuentran los archivos necesarios para el arranque del sistema.

# Directorio dev:

    Se encuentran todos los dispositivos conectados al sistema en forma de archivos.

# Directorio etc:

    Se encuentran los archivos de configuración

# Directorio lib:

    Se encuentran todas las bibliotecas para los módulos del sistema y aplicaciones.

# Directorio media:
        
    Se encuentran todos los puntos de montaje cuando se conectan unidades externas

# Directorio proc:
        
    Se encuentran los procesos y aplicaciones que se están ejecutando en el sistema, son archivos virtuales.

# Directorio srv:

    Se encuentran archivos relacionados a servidores instalados en el equipo.

# Directorio sys:

    Contiene archivos virtuales con relación a eventos del sistema, los archivos se distribuyen de forma jerárquica.

# Directorio usr(user source resource):

    Contiene aplicaciones y archivos utilizados por los usuarios 

# Directorio var:

    Contienen los logs del sistema y aplicaciones

# Para ver la IP
    
    hostname -i

# Hacer un upgrade en Parrot

    parrot-upgrade

# Buscar archivos que sean ejecutables por root

    find / -user root -writable 2>/dev/null
    find / -user root -executable 2>/dev/null

# Buscar un archivo usando un wildcard

    find / -name dex\* 2>/dev/null

# Para que funcione el CTRL + L en la terminal, modificamos la variable de entorno

    export TERM=xterm

# Conectarse por ssh con sshpass

    sshpass -p 'PASSWORD' ssh username@x.x.x.x [PORT]

# Grepeando trucos

    grep -r "\w" 2>/dev/null | tail -n1 | awk '{print $2}' FS=":"
    grep -r "\w" 2>/dev/null | tail -n1 | awk '{print $NF}' FS=":"
    grep -r "\w" 2>/dev/null | tail -n1 | tr ":" " " | awk 'NF{print $NF}'
    echo -e "\n[+] La contraseña es: $(grep -r "\w" 2>/dev/null | tail -n1 | awk '{print $NF}' FS=":")\n"
    find . -type f | grep "\-f" | xargs file
    find . -type f -readable -size 1033c | xargs cat | head -n1 
    find / -user bandit7 -group bandit6 -size 33c 2>/dev/null | xargs cat
    cat data.txt | grep "millionth" | awk 'NF{print $NF}'
    cat data.txt | grep "millionth" | xargs  | cut -d ' ' -f 2
    cat data.txt | grep "millionth" | xargs | tr ' ' '\n' | tail -n1

# Listar líneas únicas

    sort data.txt | uniq -u

# Imprime la cadena de caracteres imprimibles

    strings [FILE] 

# Ejemplo de comando con 'awk'

    strings data.txt | grep "===" | tail -n1 | awk 'NF{print $NF}

# Convertir una cadena en base64

    echo "Hola, esto es una prueba" | base64

# Convertir una cadena en base64 en una sola línea

    echo "Hola, esto es una prueba" | base64 -w 0

# Decodificar de base 64 a string

    echo "Hola, esto es una prueba" | base64 -d

# Para ver la rotación de los caracteres podemos hacer uso de la siguiente página

    https://rot13.com/

# 	 

- echo '' > /dev/tcp/127.0.0.1/23 2>/dev/null && echo "[+] El puerto esta abierto" || echo "[+] El puerto está cerrado"

- ping -c 1 10.0.0.28 2>/dev/null && echo "[+] El host esta activo." || echo "[+] El host no está activo."


- timeout 1 bash -c "ping -c 1 10.0.0.28 2>/dev/null" && echo "[+] El host esta activo." || echo "[+] El host no está activo."


# Crear un directorio temporal de trabajo

	mktemp -d

# Testear puertos

	nmap --open -T5 -v -n -p31000-32000 127.0.0.1	

# Ver la diferencias en los archivos

	diff [FILE1] [FILE2]

# Se puede ejecutar un comando con ssh

	sshpass -p hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg ssh bandit18@bandit.labs.overthewire.org -p 2220 bash

# Aprovechar saltando privilegios cuando se tiene un file setuid, se complementa con el comando bash -p para entrar a la shell del usuario

	./script.sh bash -p 

# Interesante script:

    bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
    #!/bin/bash

    myname=$(whoami)

    cd /var/spool/$myname/foo
    echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
    for i in * .*;
    do
        if [ "$i" != "." -a "$i" != ".." ];
        then
            echo "Handling $i"
            owner="$(stat --format "%U" ./$i)"
            if [ "${owner}" = "bandit23" ]; then
                timeout -s 9 60 ./$i
            fi
            rm -f ./$i
        fi
    done

# 
