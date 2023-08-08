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

Ver las estadísticas de los contenedores que están corriendo.

	docker stats

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

---

### Docker-compose

Ver la version de docker compose.

	docker-compose --version

Poner arriba con docker compose, siempre y cuando el archivo yaml esté por defecto el nombre 'docker-compose.yaml'

	docker-compose up

Poner arriba con docker compose, cuando tiene un nombre diferente a 'docker-compose.yaml'

	docker-compose up -f [FILE.yaml]

Poner abajo con docker compose

	docker-compose down

Listar los docker-compose en ejecución.

	docker-compose ps

Listar todos los docker-compose.

	docker-compose ps -a

---

### Redes en docker

Listar las redes de Docker

	docker network ls

Ejemplo de ejecutar un contenedor

	docker run -tid --rm --name thor busybox

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

#### MACVLAN (bridge)

Para crear una network de tipo MacVlan(bridge), este se vincula a la interface de nuestra red local. Para este ejemplo estamos utilizando la interface 'enp42s0'. Importante aquí es poder establecer un rango de IP's ya que al asignarlo autmáticamente a los containers puede haber conflicto. Esto es obviamente opcional pero es lo recomendable. El 'aux-address' es para reservar esa IP, esto prevendrá que docker use esta IP para asignar a un container.

	docker network create -d macvlan -o parent=enp42s0 \
	--subnet [x.x.x.x/x] \
	--gateway [x.x.x.x] \
	--ip-range [x.x.x.x/x] \ # opcional
	--aux-address 'host=x.x.x.x' \ # opcional
	--[NETWORK NAME]

	docker network create -d macvlan -o parent=enp42s0 \
	--subnet 10.0.0.0/24 \
	--gateway 10.0.0.30 \
	--ip-range 10.0.0.192/26 \
	--Mi_Red

La gran desventaja de **macvlan(bridge)**, es que no puede haber comunicación entre contenedores y el host. Pero podemos encontrar una solución para esto. Para esto primero crearemos una nueva interface macvlan en el host.

	ip link add [NOMBRE INTERFACE] link [INTERFACE] type macvlan mode bridge
	ip link add mynet-luis link enp42s0 type macvlan mode bridge

Establecemeos una IP en específico podemos hacerlo también.

	ip addr add [x.x.x.x/x] dev [NOMBRE INTERFACE]
	ip addr add 10.0.0.29/32 dev mynet-luis

Luego de eso ponemos arriba la interface con el siguiente comando.

	ip link set mynet-luis up

Ahora creamos una ruta para llegar al contenedor o el rango de contenedores

	ip route add [x.x.x.x/x] dev [NOMBRE INTERFACE]
	ip route add 10.0.0.192/27 dev mynet

#### MACVLAN (vlan)

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

Links

- [Docker networking is CRAZY!! (you NEED to learn it) - Network Chuck](https://www.youtube.com/watch?v=bKFMS5C4CG0&ab_channel=NetworkChuck)
