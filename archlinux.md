## Instalación de Archlinux

- loadkeys la-latin1

- iwctl

- device list

- cfdisk

- lsblk

Crear file system Ext4 para la partición root

    mkfs.ext4 /dev/sda3

Formatear a FAT32 la partición de sistema EFI. (Solo en el caso de EFI system partition)

    mkfs.fat -F 32 /dev/sda1

Inicializar la partición 'swap'

    mkswap /dev/sda2

Montar el volumen root en /mnt

    mount /dev/sda3 /mnt

Crear el directorio /mnt/boot/efi

    mkdir -p /mnt/boot/efi

Montar el 'efi system partition'.

    mount /dev/sda1 /mnt/boot/efi

Habilitar 'swap partition'

    swapon /dev/sda2

Ejecutar 'pacstrap' script para instalar el package base, linux kernel y firmware para hardware en común.

    pacstrap /mnt base linux linux-firmware sof-firmware base-devel grub efibootmgr vim networkmanager

Generar un file 'fstab'.

    genfstab -U /mnt >> /mnt/etc/fstab


