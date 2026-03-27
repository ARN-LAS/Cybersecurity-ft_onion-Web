# Cybersecurity-ft_onion-Web

# Projet ft_onion-Web

## Description

Ce projet consiste à créer un **site web statique accessible uniquement via le réseau Tor** (`.onion`).  
L’objectif est de mettre en place un **serveur web sécurisé avec NGINX**, accessible via SSH sur un port personnalisé, et de le rendre disponible sur Tor.

---

## Contenu du projet

| Fichier | Description |
|---------|-------------|
| `index.html` | Page web statique affichée sur le réseau Tor |
| `nginx.conf` | Configuration NGINX pour servir la page |
| `sshd_config` | Configuration SSH permettant l’accès sur le port 4242 |
| `torrc` | Configuration du service caché Tor (.onion) |

---

## Prérequis

- Linux (Debian/Ubuntu recommandé)  
- NGINX installé
- OpenSSH Server installé
- Tor installé (`sudo apt install tor`)  
- Tor Browser (pour tester le site .onion)

---

## Installation et configuration

### 1️⃣ Configurer NGINX

1. Copier `index.html` dans le dossier web de NGINX :

```bash
sudo cp index.html /var/www/html/index.html
Remplacer la configuration NGINX par nginx.conf :
sudo cp nginx.conf /etc/nginx/nginx.conf
sudo systemctl restart nginx
Vérifier que NGINX écoute sur le port 80 :
sudo systemctl status nginx
curl http://localhost
2️⃣ Configurer SSH
Remplacer sshd_config par le fichier fourni :
sudo cp sshd_config /etc/ssh/sshd_config
Redémarrer SSH :
sudo systemctl restart ssh
Tester la connexion SSH sur le port 4242 :
ssh user@localhost -p 4242

⚠️ Si l’utilisateur user n’existe pas :

sudo adduser user
sudo passwd user
3️⃣ Configurer Tor
Remplacer torrc par le fichier fourni :
sudo cp torrc /etc/tor/torrc
sudo systemctl restart tor
Vérifier le service caché :
sudo systemctl status tor
sudo cat /var/lib/tor/hidden_service/hostname

L’adresse .onion générée est celle à utiliser dans Tor Browser.

4️⃣ Tester le site .onion
Ouvrir Tor Browser
Entrer l’adresse .onion générée par Tor :
http://xxxxxxxx.onion
Vérifier que la page index.html s’affiche correctement.
