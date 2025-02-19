# Ubuntu 22.04 setup for robotics development
# Tested with: DELL G15 5530

This repo is a group of commands and configurations focused for preparing a fresh Ubuntu installation for robotics and ROS2 development

# install updates and reboot

```
sudo apt update & sudo apt upgrade
sudo apt autoremove & sudo apt autoclean
sudo fwupdmgr get-devices
sudo fwupdmgr get-updates
sudo fwupdmgr update
sudo reboot now
```

# install basic tools

```
sudo apt install -y vim cmake build-essential snapd arandr caffeine gparted nautilus-admin git htop ffmpeg keepass2 simplescreenrecorder locate virtualbox gimp inkscape meshlab nmap wireshark handbrake tree openssh-server
```

# install vscode
```
sudo apt-get install wget gpg apt-transport-https
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
rm -f packages.microsoft.gpg
sudo apt update && sudo apt install code
```

# install and tweak terminator
```
sudo apt install terminator
```
- scroll lines 9999999


# conky
```
sudo apt install conky -y
mkdir -p ~/.config/conky && conky --print-config > ~/.config/conky/conky.conf
install minimalistic conky theme: https://www.gnome-look.org/p/1112273/
add conky to startup programs
bash -c "sleep 10 && conky"
```

# install teams
```
sudo snap install teams-for-linux
```

# install zoom
```
cd /tmp && wget https://zoom.us/client/latest/zoom_amd64.deb
sudo dpkg -i zoom_amd64.deb
sudo apt -f install
```

# install freecad
```
sudo add-apt-repository ppa:freecad-maintainers/freecad-stable
sudo apt-get update & apt-get install freecad
```

# latex
```
sudo apt install -y texlive texlive-font-utils texlive-pstricks-doc texlive-base texlive-formats-extra texlive-lang-german texlive-metapost texlive-publishers texlive-bibtex-extra texlive-latex-base texlive-metapost-doc texlive-publishers-doc texlive-binaries texlive-latex-base-doc texlive-science texlive-extra-utils texlive-latex-extra texlive-science-doc texlive-fonts-extra texlive-latex-extra-doc texlive-pictures texlive-xetex texlive-fonts-extra-doc texlive-latex-recommended texlive-pictures-doc texlive-fonts-recommended texlive-humanities texlive-lang-english texlive-latex-recommended-doc texlive-fonts-recommended-doc texlive-humanities-doc texlive-luatex texlive-pstricks perl-tk cm-super texstudio
```

# Microsoft Fonts
## Sometimes I get documents which require fonts from Microsoft:
```
sudo apt install -y ttf-mscorefonts-installer
```

# foxit pdf reader
```
cd /tmp && wget https://cdn01.foxitsoftware.com/pub/foxit/reader/desktop/linux/2.x/2.4/en_us/FoxitReader.enu.setup.2.4.4.0911.x64.run.tar.gz
tar -vzxf  FoxitReader.enu.setup.2.4.4.0911.x64.run.tar.gz
chmod +x "FoxitReader.enu.setup.2.4.4.0911(r057d814).x64.run"
./FoxitReader.enu.setup.2.4.4.0911\(r057d814\).x64.run
```

# install utilities
## dropbox
```
sudo apt install python3-gpg
cd /tmp && wget https://www.dropbox.com/download?dl=packages/ubuntu/dropbox_2020.03.04_amd64.deb
sudo dpkg -i download\?dl\=packages%2Fubuntu%2Fdropbox_2020.03.04_amd64.deb 
sudo apt-get -f install
sudo apt-key export 5044912E | sudo gpg --dearmour -o /etc/apt/trusted.gpg.d/dropbox.gpg
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
sudo apt install -y vlc
sudo apt install -y libavcodec-extra libdvd-pkg; sudo dpkg-reconfigure libdvd-pkg
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
  
  sudo apt update
  sudo apt install docker-ce docker-compose-plugin
  sudo usermod -aG docker ${USER}
  ```
