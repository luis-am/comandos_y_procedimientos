### LVM

---

Configuracion:

- particionar discos
- crear volumenes fisicos
- crear volumenes de grupo
- crear volumenes logicos
- dar formato a los volumenes
- montar los volumenes en los directorios

Mostrar los discos actuales.

	> fdisk -l 			# mas detalle
	> lsblk 			# resumido

Adicionar discos al servidor.

Particionar discos:

		fdisk /dev/sda

		n: nueva particion
		p: imprimir la tabla de particiones
		size: +/-[#]G
		t: seleccionar el tipo de particion (8e)
		w: grabar

Crear los volumenes fisicos.

		pvcreate /dev/sda1

Visualizar los volumenes fisicos.

		pvs 		# resumido
		pvdisplay 	# mas detalle

Crear el volume group.

		vgcreate VGGroup /dev/sda1 /dev/sdc1 /dev/sdc2

Visualizar el grupo volumen logico.

		vgs
		vgdisplay

Creamos los volumenes logicos.

		# sintaxis: lvcreate -n LVdata1 -L [#] VGGroup
		lvcreate -n LVdata1 -L [#] VGGroup

		-n: name string
		-L: size

Visualizar los volumenes creados.

		lvs
		lvdisplay

Dar formato ya sea XFS o EXT4.

		mkfs.xfs /dev/VGGroup/LVdata1
		mkdir /montaje/MNTdata1
		mount /dev/VGGroup/LVdata1 /mnt/MNTdata1

Agregar los volumenes al archivo /etc/fstab.

		/dev/VGGroup/LVdata1           /montaje/data1          ext4    defaults        0 0

Montar todos los discos.

		mount -a

Desmontar todos los discos.

		umount -a

Expandir el volumen.

		lvextend -L [#G] /dev/VGGroup/LVdata1

En caso de expandir y hacer efecto la expansion ejecutar.

		xfs_growfs /mnt/database (XFS)

Utilizar el comando resize2fs.

		umount /dev/VGGroup/LVdata1
		e2fsck /dev/VGGroup/LVdata1
		resize2fs /dev/VGGroup/LVdata1
		mount /dev/VGGroup/LVdata1 /mnt/data

Reducir el volumen.

		lvreduce --resizefs -L [#] /VGGroup/LVdata1

Eliminar un volumen.

		lvremove /dev/VGGroup/LVdata1

Renombrar un volumen.

		lvrename /dev/VGGroup/LVdataOld /dev/VGGroup/LVdataNew

> WARNING: importante si se elimina un volumen se debe eliminar la entrada en el archivo /etc/fstab
