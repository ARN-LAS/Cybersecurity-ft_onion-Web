Ce projet consiste à créer un site web statique sécurisé sur le réseau Tor (.onion). L’objectif est de mettre en place un serveur web statique avec NGINX, accessible via SSH sur un port sécurisé, et disponible sur Tor pour un anonymat complet.

## Contenu du projet

- index.html : page web statique affichée sur le réseau Tor  
- nginx.conf : configuration NGINX sécurisée  
- sshd_config : configuration SSH durcie  
- torrc : configuration du service caché Tor

## Prérequis

- Linux (Debian / Ubuntu recommandé)  
- NGINX installé  
- OpenSSH Server installé  
- Tor installé (`sudo apt install tor`)  
- Tor Browser pour tester le site .onion

## Installation et configuration

1️⃣ Copier index.html dans le dossier web de NGINX :  

sudo cp index.html /var/www/html/index.html

Remplacer la configuration NGINX par nginx.conf :  

sudo cp nginx.conf /etc/nginx/nginx.conf
sudo systemctl restart nginx

Vérifier que NGINX écoute sur le port 80 :  

sudo systemctl status nginx
curl http://localhost


2️⃣ Configurer SSH sécurisé  
Copier sshd_config :  

sudo cp sshd_config /etc/ssh/sshd_config
sudo systemctl restart ssh

Créer l’utilisateur user si nécessaire :  

sudo adduser user

Connexion via SSH sur le port 4242 :  

ssh user@localhost -p 4242

🔑 Astuce : Utiliser une clé SSH pour plus de sécurité

3️⃣ Configurer Tor Hidden Service  
Copier torrc :  

sudo cp torrc /etc/tor/torrc
sudo systemctl restart tor

Récupérer l’adresse .onion :  

sudo cat /var/lib/tor/hidden_service/hostname

Accéder au site via Tor Browser :  

http://xxxxxxxx.onion


## Tester le projet

- Vérifier NGINX : `curl http://localhost`  
- Vérifier SSH : `ssh user@localhost -p 4242`  
- Vérifier Tor : ouvrir Tor Browser et entrer l’adresse .onion

## Sécurité

- Tor .onion : anonymat total, URL non indexée  
- NGINX : page statique, informations limitées  
- SSH : port 4242, root interdit, authentification par clé possible  
- Ports ouverts : uniquement 80 (HTTP) et 4242 (SSH)  
- Pour production : ajouter fail2ban, firewall et permissions strictes

## Structure finale


ft_onion-Web/
│
├─ index.html
├─ nginx.conf
├─ sshd_config
└─ torrc


## Résultat attendu

- Page statique accessible via Tor .onion  
- Serveur NGINX sécurisé  
- SSH sur port personnalisé  
- Projet simple, propre et sécurisé
