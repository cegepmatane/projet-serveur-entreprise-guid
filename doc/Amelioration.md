# Ameliorations serveur IRC 

### Personnaliser le mot d'accueil du service IRC (MOTD)

```bash
cd /etc/inspircd
# Éditer le fichier de message du jour (MOTD)
sudo jed inspircd.motd 
# Redémarrer le service pour appliquer les changements
sudo service inspircd restart 
```

### Connexion avec Weechat

```bash
# Se connecter au serveur IRC via Weechat
/connect shiftsphere
```

### Rediriger les logs

```bash
cd /etc/inspircd
# Faire une copie de sécurité de la configuration actuelle
sudo cp inspircd.conf inspircd.conf.copie-2024-02-29
# Éditer le fichier de configuration
sudo jed inspircd.conf

# Ajouter/modifier la section de logging
<log method="file" type ="* - USERINPUT -USEROUTPUT" level="default" target="/var/log/irc/log" flush="20">

cd /var/log
# Créer le fichier de log et ajuster les permissions
sudo touch irc.log
sudo chown irc:irc irc.log
# Vérifier le contenu des logs
sudo cat inspircd.log
# Redémarrer le service IRC pour appliquer les modifications
sudo service inspircd restart 
```

### Configurer la connexion de trois serveurs connus

### InspIRCd

```bash
sudo apt update
sudo apt install atheme-services

# Faire une copie de la configuration avant modification
sudo cp inspircd.conf inspircd.conf.copie-2024-03-05
# Éditer la configuration
sudo jed inspircd.conf

# Configurer les connexions entre serveurs
<link name="irc.shiftsphere.xyz" ipaddr="172.105.15.81" port="7000" allowmask="172.105.1$
<link name="irc.shiftsphere.xyz" ipaddr="172.105.15.81" port="7000" allowmask="172.$
<uline server="irc.shiftsphere.xyz" silent="yes">
<bind address="172.105.15.81" port="7000" type="servers">
<module name="spanningtree">
<module name="alias">
<module name="chghost">
<module name="mlock">
<module name="sasl">
<sasl target="services.example.tld">
<module name="servprotect">
<module name="services_account">
<module name="topiclock">

# Redémarrer InspIRCd pour appliquer les modifications
sudo service inspircd restart 
```

### Atheme Services

```bash
# Copier le fichier de configuration par défaut et ajuster les permissions
sudo cp /usr/share/doc/atheme-services/examples/atheme.conf.example /etc/atheme/atheme.conf
sudo chmod o+r -R /etc/atheme
sudo chmod o+x -R /etc/atheme
# Créer une copie de l'original pour référence
sudo cp atheme.conf atheme.conf.original
# Éditer la configuration
cd /etc/atheme
sudo jed atheme.conf
```

### Configurer et installer le jeu de loup-garou 

```bash
# Télécharger et extraire le code du jeu
wget https://github.com/lykoss/lykos/archive/refs/tags/stable-201905.zip
unzip stable-201905.zip 
mv lykos-stable-201905 lykos
cd lykos
# Installer les dépendances
python3 -m pip install -r requirements.txt

# Configurer le bot
cp botconfig.py.example botconfig.py
jed botconfig.py

# Configuration des détails du bot
HOST = "irc.quebec.agency"
PORT = 6667
NICK = "botloupgarou"
IDENT = NICK
REALNAME = NICK
USERNAME = ""  # Peut rester vide si identique à NICK
PASS = "testtest" # Peut être None si authentification avec certificats clients
SASL_AUTHENTICATION = False
USE_SSL = False
SSL_VERIFY = False
CHANNEL = "#cafe"

# Démarrer le bot
python3 wolfbot.py &
```