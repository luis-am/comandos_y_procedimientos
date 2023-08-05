## Configuraciónd de GNS3

change keyboard-layout

	sudo loadkeys es

Change console-font

	sudo setfont /usr/share/consolefonts/Lat7-TerminusBold20x10.psf.gz

Edit virtual network (virbr0 interface)

	virsh net-edit default

	<network>
      <name>default</name>
      <uuid>67b2eb35-f794-4809-8acf-7c9f9ea777a3</uuid>
      <forward mode='nat'/>
      <bridge name='virbr0' stp='on' delay='0'/>
      <mac address='52:54:00:7b:50:93'/>
      <ip address='192.168.100.1' netmask='255.255.255.0'>
        <dhcp>
          <range start='192.168.100.2' end='192.168.100.50'/>
        </dhcp>
      </ip>
    </network>

edit eth0

	sudo nano /etc/netplan/00-installer-config.yaml

	network:
  		ethernets:
		  eth0:
            dhcp-identifier: mac
            dhcp4: no
            addresses: [192.168.10.1/24]
            gateway4: 192.168.10.254
            nameservers:
              addresses: [8.8.8.8,8.8.4.4]
		version: 2

Edit ciphers in file ssh/.config
	
	Host *
	Ciphers aes256-ctr,aes128-ctr,aes256-cbc,aes128-cbc,3des-cbc KexAlgorithms diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1

Make containers persistent

- /bin
- /boot
- /dev
- /etc
- /gns3
- /gns3volumes
- /home
- /lib
- /lib64
- /root
- /sbin
- /var
- /usr
