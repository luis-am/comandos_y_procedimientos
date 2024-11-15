## Comandos 'iptables'

- Listar las reglas en un formato legible.

	iptables -nL -v
    n: numeric
    L: listar
    v: verbose

- Poner predeterminado las reglas

    sudo iptables -P INPUT DROP
    sudo iptables -P FORWARD DROP
    sudo iptables -P OUTPUT DROP

- Agregar una regla

    sudo iptables -A INPUT -p tcp --sport 80 -j ACCEPT
    sudo iptables -A INPUT -p tcp --sport 443 -j ACCEPT
    sudo iptables -A INPUT -p icmp -j ACCEPT

- Path de configuracion persistente

    /etc/iptables/rules.v4
    /etc/iptables/rules.v6

- Eliminar una regla

    sudo iptables -D INPUT [NUMBER]
    example: sudo iptables -D INPUT 3
