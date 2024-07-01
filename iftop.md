## Comandos de iftop

# Visualizar uso de ancho de banda en tiempo real en la interface por defecto

    iftop

# Seleccionar la interface [ -i ]

    iftop -i enp42s0

# No resolver el hostname [ -n ]

    iftop -n -i enp42s0

# No resolver los puertos a servicios [ -N ]

    iftop -n -N -i enp42s0

# Ver el resultado en formato de texto [ -t ]

    iftop -n -N -t -i enp42s0

# Ver el resultado seleccionando el origen [ -F ]

    iftop -n -N -F [SOURCE]

# Ejemplo muy útil

	iftop -Nnm 10M -F 172.16.16.17/32 -i Port1
