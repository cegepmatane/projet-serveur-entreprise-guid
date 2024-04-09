# Procedure serveur IRC 

```bash
sudo apt install inspircd 
sudo ufw allow 6667/tcp
sudo ufw reload 
```

**Panneau Porkpon**

```bash
CNAME irc.shiftsphere.xyz

sudo chmod +x /etc/inspircd
sudo cp inspircd.conf inspircd.conf.copie 

sudo jed inspircd.conf
sudo service inspircd restart 

sudo apt install weechat
```

**weechat** 

```bash
/serveur add shiftsphere irc.shiftsphere.xyz/6667
/connect shiftsphere
/join #cafe
```