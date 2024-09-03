## Uso del comando "virsh", herramienta para gestionar máquinas virtuales en la shell.

# Listar máquinas virtuales activas

	virsh list

# Listar todas las máquinas virtuales
	
	virsh list --all

# Iniciar la máquina virtual

	virsh start [NOMBRE DE LA MÁQUINA VIRTUAL]	

# Apagar la máquina virtual
	
	virsh shutdown [NOMBRE DE LA MÁQUINA VIRTUAL]	

# Ver información de la máquina virtual
	
	virsh dominfo [NOMBRE DE LA MÁQUINA VIRTUAL]	

# Eliminar la máquina virtual
	
	virsh undefine [NOMBRE DE LA MÁQUINA VIRTUAL]	

# Listar todas las redes

	virsh net-list --all

# Definir una nueva red desde un archivo XML

	virsh net-define [XML FILE]

# Crear e iniciar una red desde un archivo XML

	virsh net-create [XML FILE]

# Iniciar una red definida

	virsh net-start [NOMBRE DE LA RED]

# Detener una red definida

	virsh net-destroy [NOMBRE DE LA RED]

# Eliminar una red definida

	virsh net-undefine [NOMBRE DE LA RED]

# Autoiniciar una red al inicio del sistema

	virsh net-autostart [NOMBRE DE LA RED]

# Autoiniciar una red al inicio del sistema

	virsh net-autostart [NOMBRE DE LA RED] --disable

# Obtener información de una red

	virsh net-info [NOMBRE DE LA RED]

# Obtener información de una red en formato XML

	virsh net-dumpxml [NOMBRE DE LA RED]

# Editar la configuración de una red en formato XML

	virsh net-edit [NOMBRE DE LA RED]

# Listar los dispositivos de filtro de red

	virsh nwfilter-list

# Definir un nuevo filtro de red desde un archivo XML

	virsh nwfilter-define [XML FILE]

# Eliminar un filtro de red

	virsh nwfilter-undefine [FILTER NAME]

# Obtener detalles de un filtro de red en formato XML

	virsh nwfilter-dumpxml [FILTER NAME]

-------------------------------------------------------------------

## Clonar una máquina virtual con la herramienta "virt-clone"

# Identificar la máquina virtual y su configuración

	virsh list --all
	virsh dumpxml [VM NAME]

# Clonar máquina virtual

	virt-clone --original [VM NAME] --name [NEW VM NAME] --file /var/lib/libvirt/images/[NEW VM NAME].qcow2

# Verificar la nueva máquina virtual

	virsh list --all

-------------------------------------------------------------------

## Crear snapshots

# Listar las máquinas virtuales

	virsh list --all

# Crear un snapshot

	virsh snapshot-create-as [VM NAME] [SNAPSHOT NAME] "SNAPSHOT DESCRIPTION" --disk-only --atomic

# Listar los snapshots

	virsh snapshot-list [VM NAME]

# Revertir un snapshot (Máquina tiene que estar apagada.)

	virsh snapshot-revert [VM NAME] [SNAPSHOT NAME]

# Eliminar un snapshot

	virsh snapshot-delete [VM NAME] [SNAPSHOT NAME]

-------------------------------------------------------------------

## Ruta para los archivos XML para las máquinas virtuales y las redes virtuales.

	/etc/libvirt/qemu/ → máquinas virtuales
	/etc/libvirt/qemu/networks/ → redes virtuales
	/etc/libvirt/qemu/nwfilter/ → filtros de red

-------------------------------------------------------------------

## Extender un disco.

# Determinar la ruta del disco de la máquina virtual

	virsh domblklist [VM NAME]

# Ver información del disco 

	sudo qemu-img info /var/lib/libvirt/images/[DISK].qcow2

# Extender el tamaño del disco de la máquina virtual (Por ejemplo 20G)	

	sudo qemu-img resize /var/lib/libvirt/images/[DISK].qcow2 +20G
