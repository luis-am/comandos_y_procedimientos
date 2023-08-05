### RAID 6

Instalar mdadm.

	sudo apt install mdadm

Ver las particiones.

	sudo cat /proc/partitions

Verificar los bloques.

	sudo mdadm -E /dev/sd[bcdef]

Ejecutar fdisk y crear la particion, en tipo escoger "fd" que es del tipo "Linux Raid Autodetect".

Informar al OS del cambio de la tabla de particiones.

		partprobe

Ejecutar el comando mdadm para crear el raid, donde '--level' es el nivel 6, y '--raid-devices' son los dispositivos que conforman el raid.

	mdadm --create /dev/md0 --level=6 --raid-devices=5 /dev/sd[bcdef]1

Visualizar la sincronizacion del raid.

		cat /proc/mdstat

Ejecutar un comando que cada un segundo muestre la sincronizacion.

		watch -n1 cat /proc/mdstat

Ver con mas detalle el dispositivo creado del raid.

		mdadm --detail /dev/md0

Crear el file system al dispositivo raid.

		mkfs.ext4 /dev/md0

Creamos una carpeta y lo montamos en ella.

		mkdir /mnt/raid6
		mount /dev/md0 /mnt/raid6/

Añadir el disco en el archivo /etc/fstab (lo de siempre)

Que los detalles se copien al archivo mdadm.conf.

		mdadm --detail --scan --verbose >> /etc/mdadm.conf

Añadir un disco a un raid ya creado.

		mdadm --add /dev/md0 /dev/sdg

Actualizar initramfs para que obtenga los ajustes durante el boot

		update-initramfs -u
