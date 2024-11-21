## Comandos de snmpwalk

- Ver el string del host ejecutando snmp.

    snmpwalk -v 2c -c public [IP ADDRESS] 1.3.6.1.2.1.1.5.0
    snmpwalk -v 2c -c public 192.168.122.1 1.3.6.1.2.1.1.5.0

- Ataque de fuerza bruta para obtener el community string usando un diccionario.

    onesixtyone -c [DICCIONARIO] [IP ADDRESS]
    onesixtyone -c dict.txt 192.168.122.1

    -c: community file

- 
