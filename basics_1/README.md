📁 basics_1 — Révision Réseau & Scripting Bash
Ce dossier contient des scripts Bash permettant de manipuler et observer le comportement réseau sur une machine Ubuntu. Très utile pour comprendre la résolution DNS, les interfaces IP, les sockets, et plus !

✅ 0. Change your home IP
Fichier : 0-change_your_home_IP
Objectif :

Rediriger localhost vers 127.0.0.2

Forcer facebook.com à se résoudre vers 8.8.8.8

Utilisation :

bash
Copier le code
chmod +x 0-change_your_home_IP
sudo ./0-change_your_home_IP
Vérification :

bash
Copier le code
ping localhost         # doit pointer vers 127.0.0.2
ping facebook.com      # doit pointer vers 8.8.8.8
Attention : cela modifie /etc/hosts. Revenir à l’état normal ensuite.

🔄 Reset Script (optionnel)
Fichier proposé : reset_hosts.sh
Permet de :

Restaurer localhost à 127.0.0.1

Supprimer la redirection forcée de facebook.com

✅ 1. Show attached IPs
Fichier : 1-show_attached_IPs
Objectif : Afficher toutes les adresses IPv4 actives.

Script :

bash
Copier le code
#!/bin/bash
ip -4 addr show | grep -oP '(?<=inet\s)\d+(\.\d+){3}'
Utilisation :

bash
Copier le code
chmod +x 1-show_attached_IPs
./1-show_attached_IPs | cat -e
Exemple de sortie :

ruby
Copier le code
127.0.0.1$
10.255.255.254$
172.17.36.61$
✅ 2. Port listening on localhost
Fichier : 2-port_listening_on_localhost
Objectif : Écouter sur le port 98 de localhost pour recevoir du texte.

Script :

bash
Copier le code
#!/bin/bash
nc -l -s 127.0.0.2 -p 98
Utilisation :

🖥️ Terminal 1 :

bash
Copier le code
sudo ./2-port_listening_on_localhost
📡 Terminal 2 :

bash
Copier le code
telnet localhost 98
Tape du texte dans le Terminal 2 → s'affiche dans le Terminal 1.

Dépendance :

bash
Copier le code
sudo apt install netcat
🧠 Astuces de révision
Le fichier /etc/hosts permet d’écraser la résolution DNS normale.

127.0.0.1, 127.0.0.2... → tous sont en local (loopback).

ip addr et netstat, ss, nc sont indispensables pour diagnostiquer un réseau.

telnet et nc permettent de tester des connexions entre ports.

