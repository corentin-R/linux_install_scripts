# Install Raspberry memo

## SSH key server
https://www.ssh.com/ssh/copy-id

## Oh-my-zsh

https://github.com/robbyrussell/oh-my-zsh

git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
chsh -s /bin/zsh
theme: gallifrey

## Install common tools
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install vim git zsh 

## Install samba

https://www.place4geek.com/blog/2017/02/tuto-raspberry-pi-partager-un-disque-dur-en-reseau-faire-un-nas/

sudo apt-get install samba samba-common-bin
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.old
sudo vim /etc/samba/smb.conf



#Configuration générale
[global]
   workgroup = WORKGROUP
   server string = %h server

   # nom de votre NAS
   netbios name = MONNAS
   dns proxy = no

   # un endroit pour stocker les logs / debug
   log file = /var/log/samba/log.%m
   max log size = 1000
   syslog = 0
   panic action = /usr/share/samba/panic-action %d

   # Authentication

   security = user
   encrypt passwords = true
   passdb backend = tdbsam
   obey pam restrictions = yes
   unix password sync = yes
   passwd program = /usr/bin/passwd %u
   passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
   pam password change = yes
   map to guest = bad user
   usershare allow guests = yes

# Nos différents partages : vous pouvez en créer plusieurs à partir de ces 3 modèles selon vos besoins
[Public]
   path =/home/pi/NAS/Public
   read only = no
   locking = no
   guest ok = yes
   force user = pi

[Films]
   path =/home/pi/NAS/Films
   read only = yes
   locking = no
   guest ok = yes
   force user = pi

[Perso]
   browseable = no
   path = /home/pi/NAS/Perso
   writable = yes
   username = Toto
   only user = yes
   create mode = 0600
   directory mask = 0700


sudo mkdir /home/pi/NAS
sudo mkdir /home/pi/NAS/Public
sudo mkdir /home/pi/NAS/Films
sudo mkdir /home/pi/NAS/Perso



sudo chmod 777 -R /media/NAS


