### wifi_manager.md

---

Listar las redes Wi-Fi disponibles

    nmcli device wifi list

Conectarse a una red wifi nueva

    nmcli device wifi connect [SSID]

Conectarse a una red wifi

    nmcli device connect [INTERFACE NAME]

Desconectarse a una red wifi

    nmcli device disconnect [INTERFACE NAME]

Desactivar el autoconnect

    nmcli device set [INTERFACE NAME] autoconnect [yes|no]

Muestra la información de configuración inalámbrica

    iwconfig

Activar/desactivar la interface inalámbrica

    sudo ifconfig [INTERFACE NAME] [up|down]
