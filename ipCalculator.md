Procedimiento para subnetear (VLSM):

Dada la siguiente red: 10.64.0.0/10, se debe crear 7 subredes con los siguientes tamaños de hosts:

Subred A: 4012
Subred B: 3000
Subred C: 2500
Subred D: 2200
Subred E: 800
Subred F: 200
Subred G: 17

Paso 1:
Subred A: 10.64.0.0/10
    4012 < 4096 → 2^12 = 4096 → 32 - 12 = 20
Subred A: 10.64.0.0/20 tiene 4096 hosts.
4096 / 256 = 16

Subred B: 10.64.16.0/...
    3000 < 4096 → 2^12 = 4096 → 32 - 12 = 20
Subred B: 10.64.16.0/20
4096 / 256 = 16

Subred C: 10.64.32.0/...
    2500 < 4096 → 2^12 = 4096 → 32 - 12 = 20
Subred C: 10.64.32.0/20
4096 / 256 = 16

Subred D: 10.64.48.0/...
    2200 < 4096 → 2^12 = 4096 → 32 - 12 = 20
Subred D: 10.64.48.0/20
4096 / 256 = 16

Subred E: 10.64.64.0/...
    800 < 1024 → 2^10 = 1024 → 32 - 10 = 22
Subred E: 10.64.64.0/22
1024 / 256 = 4

Subred F: 10.64.68.0/...
    200 < 256 → 2^8 = 256 → 32 - 8 = 24
Subred F: 10.64.68.0/24
256 / 256 = 1

Subred G: 10.64.69.0/...
    17 < 32 → 2^5 = 32 → 32 - 5 = 27
Subred G: 10.64.69.0/27
