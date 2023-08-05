tarea:
	webmin, investigar sobre enp0s3, explicar que significa fstab

*** apagar un servidor linux desde linux ***
	input: shutdown -h now init 0
*** reiniciar la tarjeta
	input: systemctl restart network
*** ruta de configuracion de adaptador
	path: /etc/sysconfig/network-scripts/ifcfg-enp0s3
*** ve la ip y la mascar
	input: ip address
*** ver el gateway
	input: ip route
	input: route -n
		-n: numeric
	input: netstat -rn
		-n: numeric
		-r: route
*** ver los paquetes instalados
	input: rpm -qa
		-q: query
		-a: all
*** ver la cantidad de paquetes instalados
	input: rpm -qa | wc -l
*** ver la version de linux
	input: cat /etc/redhat-release
*** instalar el paquete net-tools
	input: yum install net-tools
*** para ver el dns
	input: cat /etc/resolv.conf
*** instalar el paquete bind-utils
	input: yum install bind-utils
*** consulta dns
	input: nslookup x.x.x.x/x
*** consulta los usuarios que pertenecen a un grup
	input: lid -g mail
		-g: group
--------- 1:01:09
*** LVM → logical volume manager
*** ver el archivo acerca de la informacion de los filesystem
	input: cat /etc/fstab
*** ver los file system
	input: df -h
*** crea con 2 discos nuevos un file system ext4 de 10gb y otro file system xfs de 5GB
	el disco de 10gb debe estar montado en /opt
	el disco de 5gb debe estar montado en /data
*** nombrar los discos
	input: fdisk -l
		-fdisk: manipular particiones de disco
		-l: listar
	input: lsblk
		lsblk - list block devices
	input: blkid
		blkid - locate/print block device attributes
*** ubicacion de los discos
	input: ls -l /dev/sd*
*** dar formato a un disco
	input: mkfs -t ext4 /dev/sdb
		-mkfs: make filesystem
		-t: type
*** montar un file system en un directorio
	input: mount /dev/sdb /opt
	input: mount /dev/sdc /data

// si reiniciamos al ejecutar el comando df -h no se
// visualizan los discos, para visualizar y que sea persistente
// tenemos que añadir los discos al archivo /etc/fstab,
// añadir las siguientes lineas
	input: /dev/sdb	/opt 	ext4 	defaults 0 0
	input: /dev/sdc	/media	xfs 	defaults 0 0
// luego ejecutar el comando:
	input: mount -a
		-a: all
// desmontar un disco
	input: sudo unmount /dev/sda
// instalar ncdu
*** ver los permisos de directorio root
	input: mount | grep root
*** cambiar los permisos en un directorio de lectura, escritura
	input: mount -o remount, rw /

----- clase semana 4
*** T4BL - Tareas clase LVM
*** particionar el disco
		input: fdisk /dev/sdb1
		wizard: Command (m for help): p
		wizard: Command (m for help): n
		wizard: Select (default p): p
		Usar ID 8e, usar la opcion t para Linux LVM
		para grabar los cambios se usa w
