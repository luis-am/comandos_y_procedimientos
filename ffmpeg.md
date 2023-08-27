### ffmpeg.md

Ver información de un video

    ffmpeg -i [NAME VIDEO] -hide_banner
    ffmpeg -i video.mp4 -hide_banner

Convertir un archivo de video a otro formato

    ffmpeg -i VIDEO.mp4 VIDEO.avi
    ffmpeg -i VIDEO.mkv VIDEO.mp4

Convertir un archivo de video a otro formato sin perder calidad

    ffmpeg -i VIDEO.mp4 -qscale 0 VIDEO.avi

Comando básico para grabar solo pantalla

    ffmpeg -f x11grab -s 1366x766 -r 30 -i :0.0 output.mkv

Comando básico para grabar pantalla y audio

    ffmpeg -f x11grab -s 1366x766 -i :0.0 -f pulse -i default output.mkv

Comando básico para grabar solo audio

    ffmpeg -f pulse -i default output.mp3

Grabar webcam, podemos ver la lista de dispositivos con el comando 'ls /dev', normalmente para webcams el archiv se llama 'video#'

    ffmpeg -i /dev/video0 output.mkv
