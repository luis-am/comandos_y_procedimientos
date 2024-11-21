## Comandos de gobuster

- Fuerza bruta a directorio/files [ Directory/File Enumeration ]

    gobuster dir -u http://[IP ADDRESS] -w [WORDLIST]
    gobuster dir -u http://10.10.10.121/ -w /usr/share/seclists/Discovery/Web-Content/common.txt

    dir: modo fuerza bruta de directorio
    -u: url
    -w: wordlist

- DNS subdominio enumeración

    git clone https://github.com/danielmiessler/SecLists
    sudo apt install seclists -y
    echo "1.1.1.1" >>  /etc/resolv.conf

    gobuster dns -d [DOMAIN NAME] -w [LIST FILE]
    gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt
    
