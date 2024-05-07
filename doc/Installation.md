### Installation et configuration de InspIRCd

- Installation d'InspIRCd

```bash
# Installer le serveur IRC InspIRCd
sudo apt install inspircd
```

- Configuration du pare-feu

```bash
# Autoriser le trafic sur le port standard IRC
sudo ufw allow 6667/tcp
# Recharger la configuration du pare-feu pour appliquer les changements
sudo ufw reload
```

### Configuration initiale d'InspIRCd

- Préparation des fichiers de configuration

```bash
# Donner les permissions d'exécution au répertoire de configuration
sudo chmod +x /etc/inspircd
# Créer une copie de sécurité du fichier de configuration par défaut
sudo cp /etc/inspircd/inspircd.conf /etc/inspircd/inspircd.conf.copie
```

- Édition de la configuration

```bash
# Éditer le fichier de configuration
sudo jed /etc/inspircd/inspircd.conf
```

- Redémarrage d'InspIRCd

```bash
# Redémarrer le service InspIRCd pour appliquer les modifications
sudo service inspircd restart
```

### Installation de WeeChat

```bash
# Installer WeeChat, un client IRC populaire
sudo apt install weechat
```

### Configuration de WeeChat pour se connecter au serveur

- Ajouter le serveur à WeeChat

```bash
# Ajouter le serveur IRC à WeeChat
/server add shiftsphere irc.shiftsphere.xyz/6667
```

- Connexion au serveur

```bash
# Se connecter au serveur ajouté
/connect shiftsphere
```

- Rejoindre un canal

```bash
# Rejoindre le canal #cafe
/join #cafe
```