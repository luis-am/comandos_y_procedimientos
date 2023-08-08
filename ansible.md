## Comandos de Ansible

- Michael DeHaan inventó Ansible

- Ansible fue creado en 2012

- Ansible fue adquirido por Red Hat en 2015

- Con Ansible podemos tener todo tipo de targets desde servidores, hosts, switches, routers, contenedores, etc.

- Los componentes principales de Ansible son Ansible executable, módulos, playbooks(es un libro en donde está la configuración, inventarios son una colección de targets).

- El algoritmo usado para crear las llaves simetricas en la autenticación por SSH es Diffie-Hellman

- La opción ssh 'StrictHostKeyChecking=no' es para aceptar de manera automática fingerprints de desconocidos.

### Teoría

Un **inventario** es la lista de hosts o nodos en el cual se desea gestionar la configuración y la automatización. Este inventario tiene detalles de los hosts, como direcciones IP, nombres y los grupos al cual pertenecen y otras variables de configuración. 

Un **playbook** es un archivo en formato YAML que contiene las instrucciones para definir y ejecutar las tareas a un determinado target. Cada playbook puede tener una o más tareas

---

Ruta del archivo de configuracion de ansible

	/etc/ansible/ansible.cfg
	~/.ansible.cfg

Probar conectividad a los hosts una vez haya configurado la autenticacion por ssh desde el cliente ansible; '-i' significa inventario, 'm' significa módulo, el grupo por defecto es 'all', este se puede reemplazar por algún grupo en específico que se encuentra en el archivo 'hosts', se puede utilizar caracteres comodines, pero tienen que estar dentro de comillas simples.

	ansible [GROUP] -m [MODULE]
	ansible all -m ping
	ansible '*' -m ping
	ansible -i,ubuntu1,ubuntu2,ubuntu3,centos1,centos2,centos3 all -m ping

Ver la version de Ansible, aquí también se puede visualizar si ansible tiene un archivo de configuración.

	ansible --version
	
Creamos una variable de entorno y lo asociamos a la variable de entorno
	
	touch this_is_my_example_ansible.cfg
	export ANSIBLE_CONFIG=/home/ansible/this_is_my_example_ansible.cfg

Si en caso no hay archivo Known_hosts en .ssh se puede hacer lo siguiente, automáticamente crea el archivo ~/.ssh/known_hosts

	ANSIBLE_HOST_KEY_CHECKING=False ansible all -m ping

Ver de manera condensada el output cuando probamos conectividad a los targets

	ansible all -m ping -o
	ansible ubuntu1 -m ping -o
	
Listar los hosts de un grupo en específico en un inventario, también podemos hacerlo solo hacia un target, podemos usar también regex matching (para empezar con regex expressions iniciamos con el símbolo '~', el punto significa cualquier caracter, luego el arterisco significa cualquier cantidad de caracteres para que finalmente termine con el número '3')

	ansible [GROUP] --list-hosts
	ansible centos --list-hosts
	ansible ubuntu --list-hosts
	ansible all --list-hosts
	ansible centos1 --list-hosts
	ansible ~.*3 --list-hosts
		output: centos3
		output: ubuntu3

Ejecutar comandos en el servidor remoto con el módulo comando, para este ejemplo usaremos el comando 'id', '-a' significa argumento que va a ser pasado al módulo comando en este caso, en caso no especifiquemos el módulo, por defecto ansible utiliza el módulo 'command', tal como se muestra en el segundo ejemplo.

	ansible all -m command -a 'id' -o
	ansible all -a 'id' -o

Aquí podemos especificar el inventario

	ansible -i hosts --list-hosts
	ansible -i hosts.yaml --list-hosts
	ansible -i hosts.json --list-hosts

Podemos usar EXTRAVARS '-e' para override la configuración, por ejemplo en el archivo de configuración para conectarse al Centos1 usa el puerto 2222, en el comando vamos a override otro puerto,

	ansible linux -m ping -e 'ansible_port=22' -o


Si la salida del comando se muestra de color 'verde' significa que el resultado es exitoso. Si es 'amarillo' significa que ha sido exitoso con cambios. Si 

---

### Módulos

Setup Module: recolecta información del target

	ansible centos1 -m setup

File Module: set atributos o crear archivos en los target

	ansible all -m file -a 'path=/tmp/test state=touch'

File Module: Cambiar los permisos de un archivo con el módulo 'file', se puede combinar opciones como el segundo ejemplo.

	ansible all -m file -a 'path=/tmp/test state=file mode=600'
	ansible all -m file -a 'path=/tmp/test state=touch mode=600'

Copy Module: copia files desde ya sea el local o remoto target hacia algún lugar del target remoto, la opción 'remote_src=yes' sirve para copiar desde archivos remotos de targets a otros targets.
	
	touch /tmp/x
	ansible all -m copy -a 'src=/tmp/x dest=/tmp/x'
	ansible all -m copy -a 'remote_src=yes src=/tmp/x dest=/tmp/y'

Command Module: ejecuta comandos, este es el módulo por defecto.

	ansible all -a 'hostname'

Command Module: para crear archivos, y también para remover archivos.

	ansible all -a 'touch /tmp/test_command_module creates=/tmp/test_command_module'
	ansible all -a 'rm /tmp/test_command_module removes=/tmp/test_command_module'
	ansible all -m fetch -a 'src=/tmp/my_custom_file.py dest=/tmp/' -o

Para ver la información de un módulo
	
	ansible-doc [MODULE]
	ansible-doc command
	ansible-doc file

---

### Playbooks

Playbooks pueden ser escritos en YAML o JSON, que son lenguajes de serialización.

- Every YAML file should start with three dashes.
- Every YAML file should end with three dots.
- 2 espacios de indentación es lo convencional en YAML.

Cada vez que ejecutamos un playbook siempre se realiza la tarea del módulo 'setup' que recolecta información. 

	TASK [Gathering Facts] ******************************************************************************
	ok: [centos1]
	lok: [centos3]
	ok: [centos2]

Para ejecutar un playbook, y ese playbook necesita de la contraseña sudo, añadimos el switch '-K'.

	ansible-playbook playbook.yaml -K

---

### Módulo 'file' 

	tasks:
	  -name: crear nuevo archivo con permisos
	  file:
	    path:/path/to/create/file.txt
		state: touch
		mode: 0421
		owner: owner
		group: group

Links

- [Simple automation for all your Linux servers with Ansible - Christian Lempa](https://www.youtube.com/watch?v=uR1_hlHxvhc&ab_channel=ChristianLempa)
