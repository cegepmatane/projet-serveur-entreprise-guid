# Ameliorations serveur IRC 

### Personnaliser le mot d'accueil du service

cd /etc/inspircd
sudo jed inspircd.motd 
sudo service inspircd restart 

weechat
- /connect shiftsphere

### Rediriger les logs 

cd /etc/inspircd
sudo cp inspircd.conf inspircd.conf.copie-2024-02-29
sudo jed inspircd.conf

<log method="file" type ="* - USERINPUT -USEROUTPUT" level="default" target="/var/log/irc/log" flush="20">

cd /var/log
sudo touch irc.log
sudo chown irc:irc irc.log
sudo cat inspircd.log
sudo service inspircd restart 