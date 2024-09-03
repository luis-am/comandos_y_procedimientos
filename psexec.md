# Comandos de PSExec

Permite ejecutar comandos en equipos remotos.

## Requisitos en el equipo remoto
    - Puerto 445/TCP abierto
    - Puerto 137/UDP abierto
    - Credenciales del equipo remoto
    - Servicio "Remote Service Management (RPC) abierto"

## Paso 1
    - Habilitar Windows Firewall
    - Permitir PsExec puertos en Windows Firewall
    - Si se está dentro del dominio realizar una GPO

## Ejemplos
    Sintaxis básica
    - psexec \\remotecomputer command [arguments]
    - psexec \\remotepc ipconfig
    - psexec \\remotepc1,remotepc2 ipconfig
    - psexec \\remotepc1 -u user1 -p password1 ipconfig
    - psexec \\remotepc1 tasklist
    - psexec \\remotepc1 taskkill /pid xxxx /f

    - psexec \\remote_computer_name -u remote_user -p remote_password xcopy \\local_machine\shared_folder\file.txt C:\destination\folder\
