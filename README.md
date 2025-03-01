# Ubuntu 24.04 setup for robotics development
# Tested with: DELL G15 5530

This repo is a group of commands and configurations focused for preparing a fresh Ubuntu installation for robotics and ROS2 development

# Update Nvidia drivers BEFORE first login

The default version of Ubuntu 24.04.02 from Feb2025 (https://ubuntu.com/download/desktop) comes with kernel 6.11, which seems to work ok with the G15 5530. However, its impossible to login to Gnome without updating the Nvidia drivers. 
This configuration worked for me with, including CUDA. 

I recommend opening TTY4 (alt+control+f4), install openssh-sever and then log-in remotely and run all the commands from there:
```
sudo apt install openssh-server curl
```

Then, after login in a remote computer via SSH:
```
curl -fSsL https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/3bf863cc.pub | sudo gpg --dearmor | sudo tee /usr/share/keyrings/nvidia-drivers.gpg > /dev/null 2>&1
sudo apt install build-essential gcc dirmngr ca-certificates software-properties-common apt-transport-https dkms curl -y
echo 'deb [signed-by=/usr/share/keyrings/nvidia-drivers.gpg] https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/ /' | sudo tee /etc/apt/sources.list.d/nvidia-drivers.list
sudo apt update
```

```
sudo apt purge *nvidia*
sudo apt install nvidia-driver-570-open cuda-drivers-570 cuda-12-8
sudo apt install nvidia-cuda-toolkit
```

# Install updates and reboot

```
sudo apt update && sudo apt upgrade
sudo apt autoremove && sudo apt autoclean
sudo fwupdmgr get-devices
sudo fwupdmgr get-updates
sudo fwupdmgr update
sudo reboot now
```

# Install basic development/quality-of-life tools
```
sudo apt install -y vim cmake build-essential snapd arandr caffeine gparted nautilus-admin git htop ffmpeg keepass2 simplescreenrecorder locate virtualbox gimp inkscape meshlab nmap wireshark handbrake tree openssh-server wget gpg apt-transport-https neofetch lz4 libxml2-utils qemu-user-static
```

# Install VScode
A handy and flexible code editor! Compatible with native docker instalations. 

```
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
rm -f packages.microsoft.gpg
sudo apt update && sudo apt install code
```

# Install and tweak terminator
Best terminal for multi-tasking in robotics in my opinion!

```
sudo apt install terminator
```
Setup terminator profile to define the `scroll lines` to an absurd high number like: 9999999

# Install teams
A necessary evil.

```
sudo snap install teams-for-linux
```

# Install zoom
Another necessary evil.

```
cd /tmp && wget https://zoom.us/client/latest/zoom_amd64.deb
sudo dpkg -i zoom_amd64.deb
sudo apt -f install
```

# Install Freecad
Best open source CAD software in my opinion! This PPA has the latest version >= 1.0.

```
sudo add-apt-repository ppa:freecad-maintainers/freecad-stable
sudo apt-get update & apt-get install freecad
```

# Latex
```
sudo apt install -y texlive texlive-font-utils texlive-pstricks-doc texlive-base texlive-formats-extra texlive-lang-german texlive-metapost texlive-publishers texlive-bibtex-extra texlive-latex-base texlive-metapost-doc texlive-publishers-doc texlive-binaries texlive-latex-base-doc texlive-science texlive-extra-utils texlive-latex-extra texlive-science-doc texlive-fonts-extra texlive-latex-extra-doc texlive-pictures texlive-xetex texlive-fonts-extra-doc texlive-latex-recommended texlive-pictures-doc texlive-fonts-recommended texlive-humanities texlive-lang-english texlive-latex-recommended-doc texlive-fonts-recommended-doc texlive-humanities-doc texlive-luatex texlive-pstricks perl-tk cm-super texstudio
```

# Microsoft Fonts
Sometimes we need to open documents which require fonts from Microsoft:
```
sudo apt install -y ttf-mscorefonts-installer
```

# Foxit pdf reader
```
cd /tmp && wget https://cdn01.foxitsoftware.com/pub/foxit/reader/desktop/linux/2.x/2.4/en_us/FoxitReader.enu.setup.2.4.4.0911.x64.run.tar.gz
tar -vzxf  FoxitReader.enu.setup.2.4.4.0911.x64.run.tar.gz
chmod +x "FoxitReader.enu.setup.2.4.4.0911(r057d814).x64.run"
./FoxitReader.enu.setup.2.4.4.0911\(r057d814\).x64.run
```

# install utilities
## dropbox
```
cd /tmp && wget https://www.dropbox.com/download?dl=packages/ubuntu/dropbox_2024.04.17_amd64.deb
sudo dpkg -i download\?dl\=packages%2Fubuntu%2Fdropbox_2024.04.17_amd64.deb
sudo apt-get -f install
```

# vpn services
```
sudo apt install -y openvpn network-manager-openvpn network-manager-openvpn-gnome openconnect wireguard
```

# generate ssh key
```
ssh-keygen
```
# install sublime text
```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg > /dev/null

echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt update && sudo apt-get install sublime-text
```

# install zsh
```
sudo apt install zsh zsh-syntax-highlighting
chsh -s $(which zsh)
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
sh -c "$(curl -fsSL https://git.io/zinit-install)"

-- add to the end of ~/.zshrc
zinit light zdharma/fast-syntax-highlighting
zinit light zsh-users/zsh-autosuggestions
zinit light zsh-users/zsh-completions
```
https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md



# install Spotify
```
curl -sS https://download.spotify.com/debian/pubkey_C85668DF69375001.gpg | sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/spotify.gpg
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
sudo apt-get update && sudo apt-get install spotify-client
```

# fix key bindings
chrome://flags/#hardware-media-key-handling
disable

go to keyboard->customize shortcuts->play/pause
go to keyboard->customize shortcuts->next track
go to keyboard->customize shortcuts->previous track

# Multimedia
```
sudo apt install -y vlc libavcodec-extra libdvd-pkg; sudo dpkg-reconfigure libdvd-pkg
```

# OBS
```
sudo apt install -y obs-studio
```

#### instalar steam
```
cd /tmp &&  wget https://repo.steampowered.com/steam/archive/precise/steam_latest.deb
sudo dpkg -i steam_latest.deb
```
##### Fix libs
```
sudo dpkg --add-architecture i386
sudo apt-get update
sudo apt install libgl1-mesa-dri:i386 libgl1:i386
sudo apt-get upgrade steam -f
```

steam


# disable IPv6 to prevent nasty issues with ROS

https://www.reddit.com/r/pop_os/comments/jkgwbe/having_problems_with_getting_your_vpn_to_work_on/
```
nano /etc/sysctl.conf
```
# Disable IPv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

sudo reboot

Check with ping6 google.com



### docker
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
  sudo apt update && sudo apt install docker-ce docker-compose-plugin
  sudo usermod -aG docker ${USER}
  ```


# Install Conky
A light-weight system monitor for X, Wayland, and other things, too. For more info check: https://github.com/brndnmtthws/conky.

```
sudo apt install conky-all -y
mkdir -p ~/.config/conky && conky --print-config > ~/.config/conky/conky.conf
```
Another steps:
- install minimalistic conky theme: https://www.gnome-look.org/p/1112273/
- add conky to startup programs
- `bash -c "sleep 10 && conky"`
