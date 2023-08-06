##  Comandos de Docker

¿Qué es una imagen?
> Es una plantilla maestra de solo lectura que se utiliza para crear contenedores que son exactamente igual. En él se contiene el código, bibliotecas y dependencias.

---

Buscar imagen

	docker search [IMAGE]

Ver los detalles de una imagen ya descargada

	docker image inspect [IMAGE]

Descargar la imagen

	docker pull [IMAGE]
	docker pull [IMAGE:VERSION]

Lista todas las imagenes que hayamos descargado

	docker images

Lista todas las imagenes que hayamos descargado mostrando el #id

	docker images ls -q 
		
Eliminar imagen descargada

	docker image rm [IMAGE]

Crear un contenedor

	docker create [IMAGE]
	docker container create [IMAGE]
	docker create --name [CONTAINER_NAME] [IMAGE]

Iniciar un contenedor

	docker start [ID CONTAINER]
	docker start [CONTAINER_NAME]

Ver que contenedores estan corriendo

	docker ps

Detener contenedor que esta corriendo

	docker stop [CONTAINER ID]

Detener todos los contenedores que estan corriendo

	docker stop $(docker ps -q)

	-q: quiet, solo muestra los id's de los contenedores, que luego se pasan
		como argumentos del comando 'docker stop'

Ver que contenedores activos/inactivos del sistema

	docker ps -a

Eliminar un contenedor en base al nombre/id

	docker rm [CONTAINER_NAME]
	docker rm [ID CONTAINER]

Mapear puertos

	docker create -p[LOCAL PORT]:[CONTAINER PORT] --name [CONTAINER_NAME] image

Verificar si el contenedor se ejecuto correctamente

	docker logs [CONTAINER_NAME]
	docker logs --follow [NAME CONTAINER]

Crear contenedor, ejecutar de manera rapida

	docker run [IMAGE]

Crear contenedor, ejecutar de manera rapida sin mostrar los logs

	docker run -d [IMAGE]

Listar los contenedores de manera resumida

	docker ps -aq

Listar todas las redes

	docker network ls

Crear una red

	docker network create [CONTAINER_NAME]

Eliminar una red

	docker network rm [CONTAINER_NAME]

Ver la version de docker compose

	docker-compose --version

Ejemplo para nginx

	docker run -d -p 8080:80 -v /nginx-html/:/usr/share/nginx/html --name web nginx
	docker run -itd --rm -p 8080:80 --name [NAME] [IMAGE]

Ejemplo para postgre

	docker run --name [CONTAINER_NAME] -e POSTGRES_PASSWORD=[PASSWORD] -d -p 5432:5432 postgres

Ejemplo para mysql

	docker run --name [CONTAINER_NAME] -e MYSQL_ROOT_PASSWORD=[PASSWORD] -d -p 3306:3306 mysql:tag
	docker exec -it [CONTAINER_NAME] bash
	mysql -u [USERNAME] -p

Ejemplo para splunk

	docker run -d -p 8000:8000 -e "SPLUNK_START_ARGS=--accept-license" -e "SPLUNK_PASSWORD=<admin>" --name splunk splunk/splunk:latest

Arrancar contenedor de ubuntu en su terminal

	docker run -ti --name [CONTAINER_NAME] ubuntu

Arrancar contenedor de ubuntu dettach mode

	docker run -dti --name [CONTAINER_NAME] ubuntu

Attach a un contenedor

	docker attach [CONTAINER_NAME]

Dettach desde un contenedor corriendo

	ctrl+p,ctrl+q

Ejecutar un comando desde la shell al contenedor

	docker exec [NAME_CONTAINER] [COMMAND]

Directorio en donde se guardan las imagenes

	/var/lib/docker/overlay2

Poner arriba con docker compose

	docker-compose up

Poner abajo con docker compose

	docker-compose down

Listar las redes de Docker

	docker network ls

Ejemplo de ejecutar un contenedor

	docker run -itd --rm --name thor busybox

		run: crear y ejecutar un contenedor a partir de una imagen.
		-i: entrada interactiva, permite interacción con el mismo.
		-t: pseudoterminal al contenedor.
		-d: ejecuta en segundo plano (modo demonio).
		--rm: contenedor se eliminará de forma automática una vez que se detenga o salga de 
		      la aplicación.
		--name: nombre del contenedor.
		-busybox: es la imagen que permite crear sistema Linux mínimo.

Para ver el status de network

	docker inspect network [TYPE]
	docker inspect network bridge

Para crear un nuevo network definido por el usuario y asignarlo a dicha network

	docker network create [NAME]	
	docker run -itd --rm --network [NAME] --name [NAME] [IMAGE]

Para asignar un contenedor a la network 'host'

	docker run -itd --rm --network host --name [NAME] [IMAGE]

Para crear una network de tipo MacVlan(bridge)

	docker network crete -d macvlan \
	--subnet 10.0.0.0/27
	--gateway 10.0.0.30
	-o parent enp42s0	
	[NETWORK_NAME]

Para crear una network de tipo MacVlan (vlan)

	docker network create -d macvlan \
	--subnet 192.168.20.0/24 \
	--gateway 192.168.20.1 \
	-o parent enp42s0.20 \
	[NETWORK_NAME]

	docker network create -d macvlan --subnet 192.168.20.0/24 --gateway 192.168.20.1 -o parent=enp42s0.20 macvlan20

Para ejecutar un contenedor teniendo como network macvlan

	docker run -itd --rm --network Kratos --ip [IP] --name [NAME] [IMAGE]
	docker run -itd --rm --network Kratos --ip 10.0.0.2 --name stormbreaker busybox

Para crear una network de tipo ipvlan (L2)

	docker network create -d ipvlan \
		--subnet 10.0.0.0/24 \
		--gateway 10.0.0.30
		-o parent enp42s0 \
		[NETWORK NAME]

Para crear una network de tipo ipvlan (L3)

	docker network create -d ipvlan \
		--subnet 192.168.10.0/24 \
		-o parent enp42s0 -o ipvlan_mode=l3 \
		--subnet 192.168.20.0/24 \
		[NETWORK NAME]

Para ejecutar un contenedor teniendo como network ipvlan(L3)

	docker run -itd --rm --network [NETWORK_NAME] --ip 192.168.10.2 --name [NAME] [IMAGE]
	docker run -itd --rm --network [NETWORK_NAME] --ip 192.168.10.2 --name host1 busybox
	docker run -itd --rm --network [NETWORK_NAME] --ip 192.168.10.3 --name host2 busybox
	docker run -itd --rm --network [NETWORK_NAME] --ip 192.168.20.2 --name host3 busybox
	docker run -itd --rm --network [NETWORK_NAME] --ip 192.168.20.3 --name host4 busybox

Para ejecutar un contenedor teniendo como network ipvlan(L2)

	docker run -itd --rm --network [NETWORK_NAME] --ip 10.0.0.2 --name [NAME] [IMAGE]
	docker run -itd --rm --network [NETWORK_NAME] --ip 10.0.0.2 --name stormbreaker busybox

Este comando es establecer la interface en modo PROMISCuo

	sudo ip link set enp42s0 promisc on

Para agregar una nueva ruta en Linux

	sudo ip route add [RED_DESTINO] via [GATEWAY]

---

### Tipos de redes en Docker

- Default Bridge
- User-Defined Bridge
- Host
- macvlan(bridge)
- macvlan(vlan)
- ipvlan(L2)
- ipvlan(L3)

---

### Estructura de un DockerFile

FROM: Cada dockerfile debe empezar con la instrucción 'FROM', esto define la imagen base para iniciar el proceso de 'build'. Para el ejemplo se utiliza como imagen padre a 'ubuntu'.

	FROM [IMAGE]
	FROM ubuntu

ENV: Establece las variables de entorno que es requerido para ejecutar el proyecto.

	ENV [KEY] [VALUE]
	ENV	HTTP_PORT='9000'	

WORKDIR: Esto dice a docker que el resto de los comandos serán ejecutados en el contexto de /app folder dentro de la imagen. En el ejemplo se creará el directorio /app en el contenedor.

	WORKDIR [/path/to/workdir]
	WORKDIR /app

RUN: Ejecuta cualquier comando en una nueva capa encima de la imagen actual y commit los resultados.

	RUN [COMMAND]
	RUN /bin/bash -c 'source $HOME/ .bashrc; echo $HOME'

ENTRYPOINT

CMD

COPY

ADD


EXPOSE

---

### Hacer persistente los datos

Ruta en donde están los volúmenes.

	/var/lib/docker/volumes/almacen/

Crear un volúmen.

	docker volume create [VOLUME_NAME]

Listar los volúmenes.

	docker volume ls

Eliminar un volúmen.

	docker volume rm [VOLUME_NAME]

Inspeccionar un volúmen.

	docker volume inspect [VOLUME_NAME]
	
Ejemplo de como vincular un volúmen a un directorio del contenedor, donde '-v', especifica el volúmen.

	docker run -it --name [NAME_CONTAINER] -v [VOLUME_NAME]:[DIRECTORY_CONTAINER] [IMAGE_NAME]
	docker run -it --name webserver -v data:/home ubuntu
