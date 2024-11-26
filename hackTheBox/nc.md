## Comandos de netcat

- Banner grabbing

    nc -nv [IP ADDRESS] [PORT]
    nc -nv 192.168.122.1 22

    -n: no resuelve nombres
    -v: verbose

- Netcat Listener

    nc -lvnp [PORT]
    nc -lvnp 1234


