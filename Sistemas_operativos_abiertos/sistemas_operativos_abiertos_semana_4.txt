Pre-requisitos
--------------
- Usar "fdisk -l", "lsblk" para mostrar los discos actuales.
Laboratorio
------------
1.- Adicionar 2 discos al servidor con tamaño de 8GB y 20GB.
/dev/sdb   (8GB)
/dev/sdc   (20GB)

2.- Vemos los discos nuevos.
#fdisk -l 
#lsblk

3.- Particionar el disco /dev/sdb en una sola partición primaria /dev/sdb1 y el disco /dev/sdc en 2 particiones primarias /dev/sdc1 y /dev/sdc2, con fdisk, escoger opción 8e (Linux LVM).

4.- Crear los Volúmenes físicos (PV)
#pvcreate /dev/sdb1
#pvcreate /dev/sdc1
	
5.- Visualizamos los Volumenes físicos creados
#pvdisplay
#pvs

6.- Creamos el grupo de volúmenes (VG) --> VGdata
#vgcreate VGdata /dev/sdb1 /dev/sdc1

7.- Visualizar el grupo de volúmenes (VGdata)
#vgdisplay VGdata
#vgs

7.1.- Creamos los volúmenes lógicos (LV)
#lvcreate -n LVdatabase -L 2G VGdata
#lvcreate -n LVdata -L 1G VGdata

8.- Visualizar el volumen lógico
#lvdisplay VGdata
#lvs

9.- Damos el formato XFS (en su guía está con EXT4).
#mkfs.xfs /dev/VGdata/LVdatabase
#mkdir /mnt/database
#mount /dev/VGdata/LVdatabase /mnt/database

#mkfs.xfs /dev/VGdata/LVdata
#mkdir /data
#mount /dev/VGdata/LVdata /data

10.- Visualizamos los puntos de montaje y espacio libre (df -h)

11.- Reiniciamos, validaremos que no cargó "/mnt/database", ni "/data", ¿Que falta?
--> Agregar el montaje del Volumen lógico creado en /etc/fstab
/dev/VGdata/LVdatabase /mnt/database xfs defaults 0 0
/dev/VGdata/LVdata /data xfs defaults 0 0

12.- Reiniciamos y ya aparece el volumen lógico montado (revisar video comando "mount -a")
#df -h

Expandir un volumen lógico
---------------------------
1.- Expandir nuestro volumen lógico a 4GB y luego a 6GB
#lvextend -L4G /dev/VGdata/LVdatabase
#lvextend -L+2G /dev/VGdata/LVdatabase

2.- Verificamos
#lvs
#lvdisplay
#df -h

3.- Aún no es efectivo el aumento a 6G, hay que ejecutar el comando "resize2fs" (para filesystem EXT4, el comando es resize2fs para EXT4 --> ver guía)
Pero estamos trabajando con file system XFS, entonces el comando es
#xfs_growfs /mnt/database

4.- Validamos
#lvdisplay
#vgs
#df -h





