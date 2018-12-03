# Fedora 29 Dell G5

## Disable Nouveau driver at boot

At boot press Ctrl+E 

Then add ```nouveau.modeset=0 rd.driver.blacklist=nouveau``` at the end of the line beginning with linux

Blaclist Nouveau permanently

```bash
echo "blacklist nouveau" >> /etc/modprobe.d/blacklist.conf
```

Rebuild  initramfs for the running kernel
```bash
dracut -fv
````

* https://ask.fedoraproject.org/en/question/117408/how-to-diable-nouveau-in-fedora27/
* https://ask.fedoraproject.org/en/question/88140/how-to-make-dracut-regenerate-initramfs-for-only-one-kernel/
* https://wiki.debian.org/fr/KernelModuleBlacklisting

## Install general softwares

Update system

```bash
sudo dnf update
```
Install basic useful softs

```bash
sudo dnf install vim zsh git gnome-tweak-tool pinta
 ```

## Oh-My-Zsh

1. Clone the repository:

```bash
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```

2. Optionally, backup your existing ~/.zshrc file:

```bash
cp ~/.zshrc ~/.zshrc.orig
```

3. Create a new zsh configuration file

You can create a new zsh config file by copying the template that we have included for you.
```bash
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
4. Change your default shell

```bash
chsh -s /bin/zsh
```
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

Install Keepass2
```bash
sudo dnf install keepass
```

Install Kee firefox extension 

https://addons.mozilla.org/fr/firefox/addon/keefox/

Download KeePassRPC.plgx

https://github.com/kee-org/keepassrpc/releases/tag/v1.8.0

Copy it in /usr/lib/keepass/

```bash
sudo cp KeePassRPC.plgx /usr/lib/keepass/
```

Relaunch Keepass

Fill code when asked



## SSD optimizations

## Install Nivia drivers

## VS Code


Tutorial: 
https://code.visualstudio.com/docs/setup/linux



Install the key and repository:
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
```

```bash
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```
pdate the package cache and install the package using dnf
Update 
```bash
dnf check-update
```
Install VS Code
```bash
sudo dnf install code
```


## Syncthing

website: https://syncthing.net/
```bash
sudo dnf install syncthing
```
### Start Syncthing as systemd user service

tuto: https://docs.syncthing.net/users/autostart.html#linux

Create file /etc/systemd/user/syncthing@.service

```bash
vim /etc/systemd/user/syncthing@.service
```

and fill with this:

```bash
[Unit]
Description=Syncthing - Open Source Continuous File Synchronization
Documentation=man:syncthing(1)

[Service]
ExecStart=/usr/bin/syncthing -no-browser -no-restart -logflags=0
Restart=on-failure
SuccessExitStatus=3 4
RestartForceExitStatus=3 4

[Install]
WantedBy=default.target
```

Enable and start service

```bash
systemctl --user enable syncthing.service
systemctl --user start syncthing.service
```



To check the status of a user service:

```bash
systemctl --user status syncthing.service
```

Open browser and go to this page to manage syncthing configuration

```
http://localhost:8384/
```