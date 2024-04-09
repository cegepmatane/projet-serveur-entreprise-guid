# Ameliorations serveur IRC 

### Personnaliser le mot d'accueil du service

```bash
cd /etc/inspircd
sudo jed inspircd.motd 
sudo service inspircd restart 
```

**weechat**

```bash
/connect shiftsphere
```

### Rediriger les logs 

```bash
cd /etc/inspircd
sudo cp inspircd.conf inspircd.conf.copie-2024-02-29
sudo jed inspircd.conf

<log method="file" type ="* - USERINPUT -USEROUTPUT" level="default" target="/var/log/irc/log" flush="20">

cd /var/log
sudo touch irc.log
sudo chown irc:irc irc.log
sudo cat inspircd.log
sudo service inspircd restart 
```

## Connecters trois utilisateurs connue
### Inspircd

```bash
sudo apt update
sudo apt install atheme-services

sudo cp inspircd.conf inspircd.conf.copie-2024-03-05
sudo jed inspircd.conf

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

sudo service inspircd restart 
```

### Atheme

```bash
sudo cp /usr/share/doc/atheme-services/examples/atheme.conf.example /etc/- atheme/atheme.conf

sudo chmod o+r -R atheme
sudo chmod o+x -R atheme

sudo cp atheme.conf atheme.conf.original

cd /etc/atheme
sudo jed atheme.conf
```

**Code rapide pour supprimer en console** 

-ctrl shift 2
-ctrl w

```bash
serverinfo {
        name = "irc.shiftsphere.xyz";
        numeric = "5AA";
        netname = "ShiftsphereIRC";
        hidehostsuffix = "users";  
        adminname = "xenial";
        adminemail = "admin@irc.shiftsphere.xyz;


uplink "irc.shiftsphere.xyz" { 
        send_password = "testtest";
        receive_password = "testtest"; 
        port = 7000;  
};


nickserv {
        host = "QuebecIRC/services/NickServ";
chanserv {
        host = "QuebecIRC/services/ChanServ";
global {
        host = "QuebecIRC/services/Global";
infoserv {
        host = "QuebecIRC/services/InfoServ";
```

### Installer et configurer le Jeux de loup-garou 

```bash
wget https://github.com/lykoss/lykos/archive/refs/tags/stable-201905.zip
unzip stable-201905.zip 
mv lykos-stable-201905 lykos
cd lykos
python3 -m pip install -r requirements.txt

cp botconfig.py.example botconfig.py
jed botconfig.py
python3 wolfbot.py &

HOST = "irc.quebec.agency"
PORT = 6667
NICK = "botloupgarou"
IDENT = NICK
REALNAME = NICK
USERNAME = ""  # For authentication; can be left blank if the same as NICK.
PASS = "testtest" # can be None if authenticating with client certificates (see below)
SASL_AUTHENTICATION = False
USE_SSL = False
SSL_VERIFY = False

CHANNEL = "#cafe"

python3 wolfbot.py
```