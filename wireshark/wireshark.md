### Filtros

Paquetes FIN

    tcp.flags.fin == 1

Paquetes SYN

    tcp.flags.syn == 1

Paquetes analizados y con información extra de wireshark, estos son los que contienen información entre corchetes; ojo esto no es parte del protocolo tcp/ip. Es propio del wireshark.

    tcp.analysis.flags

Supongamos que habilito un filtro "ip.src == 192.168.56.0/24", y quiero saber cuántos endpoints o equipos están activos en esaa red.

    Statistics Menu > Endpoints > IPv4

Filtrar conversación entre dos IP's
    
    Analysis Menu > Conversation Filter > Ethernet
    Analysis Menu > Conversation Filter > IPv4
    Analysis Menu > Conversation Filter > TCP

Ver las conversaciones TCP

    Statistics Menu > Conversations > TCP

Exportar pcap en base al display mostrado (útil para reducir la carga de paquetes), puede ser por rango también.

    File Menu > Export Specified Packets

Operadores especiales

    contains
    frame contains admin

    matches
    frame matches admin

    in
    http.request.method in (GET,POST)

Filter reset flag

    tcp.flags.reset == 1

Revisar luego acerca de longtermn and ring buffer. (IMPORTANTE)

Listar las interfaces con dumpcap

    dumpcap -D

Capturar paquetes especificando la interface

    dumpcap -i [NUMBER] -w [FILE]
    dumpcap -i 1 -w captura.pcapng

Capturar paquetes con ringbuffer

    dumpcap -i [NUMBER] -w [FILE] -b filesize:[NUMBER IN KB] -b files:[NUMBER OF FILES]
    dumpcap -i 1 -w captura.pcapng -b filesize:500000 -b files:100

