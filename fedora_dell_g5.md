# Fedora 29 Dell G5

## Disable Nouveau driver at boot

https://ask.fedoraproject.org/en/question/117408/how-to-diable-nouveau-in-fedora27/
https://ask.fedoraproject.org/en/question/88140/how-to-make-dracut-regenerate-initramfs-for-only-one-kernel/
https://wiki.debian.org/fr/KernelModuleBlacklisting

## Install general softwares

sudo dnf update

sudo dnf install keepass vim zsh git gnome-tweak-tool pinta
 

## Oh-My-Zsh

1. Clone the repository:

git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh

2. Optionally, backup your existing ~/.zshrc file:

cp ~/.zshrc ~/.zshrc.orig

3. Create a new zsh configuration file

You can create a new zsh config file by copying the template that we have included for you.

cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

4. Change your default shell

chsh -s /bin/zsh

## Firefox

Remove title bar
https://askubuntu.com/questions/979968/how-to-hide-title-bar-in-firefox-57-quantum

uBlock Origin
https://addons.mozilla.org/fr/firefox/addon/ublock-origin/

Privacy Badger
https://addons.mozilla.org/fr/firefox/addon/privacy-badger17/


## Keepass

Tuto

https://hiob.fr/kee/

Install Kee firefox extension 

https://addons.mozilla.org/fr/firefox/addon/keefox/

Download KeePassRPC.plgx

https://github.com/kee-org/keepassrpc/releases/tag/v1.8.0

Copy it in /usr/lib/keepass/

sudo cp KeePassRPC.plgx /usr/lib/keepass/

Relaunch Keepass

Fill code when asked



## SSD optimizations

## Install Nivia drivers

# VS Code

https://code.visualstudio.com/docs/setup/linux

sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
dnf check-update
sudo dnf install code



