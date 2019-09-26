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

link: https://fedoramagazine.org/install-nvidia-gpu/

1. First, open up a terminal, and update your package-manager (if you have not done so already), by running:

```bash
sudo dnf update
```
2. Next, reboot with the simple command:
```bash
reboot
```
3. After reboot, install the Fedora 28 workstation repositories:
```bash
sudo dnf install fedora-workstation-repositories
```
4. Next, enable the NVIDIA driver repository:
```bash
sudo dnf config-manager --set-enabled rpmfusion-nonfree-nvidia-driver
```
5. Then, reboot again.

6. After the reboot, verify the addition of the repository via the following command:
```bash
sudo dnf repository-packages rpmfusion-nonfree-nvidia-driver info
```
If several NVIDIA tools and their respective specs are loaded, then proceed to the next step. If not, you may have encountered an error when adding the new repository and you should give it another shot.

7. Login, connect to the internet, and open the software app. Click Add-ons> Hardware Drivers> NVIDIA Linux Graphics Driver> Install.

If you’re using an older GPU or plan to use multiple GPUs, check the RPMFusion guide for further instructions. Finally, to ensure a successful reboot, set “WaylandEnable=false” in /etc/gdm/custom.conf, and make sure to avoid using secure boot.

### Test driver

Open up a terminal and close all other applications

    sudo dnf install glmark2
    glmark2
    Allow the test to run to completion for best results. Check to see if the frame rates match your expectation for your NVIDA card. If you’d like additional verification, consult the web to determine if a glmark2 benchmark has been previously conducted on your NVIDA card model and published to the web. Compare scores to assess your GPUs performance.
    If your framerates and/or glmark2 score are below expected, consider potential causes. CPU-induced bottlenecking? Other issues?


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

## Memo

Get installation date

```bash
ls -lct /etc | tail -1 | awk '{print $6, $7, $8}'
```
