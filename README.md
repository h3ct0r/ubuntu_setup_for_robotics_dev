# ubuntu_setup_for_robotics_dev
This repo is a group of commands and configurations focused for preparing a fresh Ubuntu installation for robotics and ROS2 development




# install updates and reboot

sudo apt update
sudo apt upgrade
sudo apt dist-upgrade
sudo apt autoremove
sudo apt autoclean
sudo fwupdmgr get-devices
sudo fwupdmgr get-updates
sudo fwupdmgr update
sudo reboot now

# set hybrid graphics

sudo system76-power graphics hybrid
sudo reboot now

# install basic tools


sudo apt install -y vim
sudo apt install -y snapd
sudo apt install -y arandr
sudo apt install -y caffeine
sudo apt install -y gparted
sudo apt install -y gnome-tweak-tool 
sudo apt install -y nautilus-admin
sudo apt install -y git
sudo apt install -y code
sudo apt install -y htop
sudo apt install -y ffmpeg
sudo apt install -y keepass2
sudo apt install -y simplescreenrecorder
sudo apt install -y locate
sudo apt install -y virtualbox
sudo apt install -y gimp
sudo apt install -y inkscape
sudo apt install -y meshlab
sudo apt install -y wireshark
sudo apt install -y handbrake
sudo apt install -y tree
sudo apt install -y openssh-server


# install and tweak terminator

sudo apt-get update
sudo apt install terminator
scroll lines 9999999
font to size 10

# conky
sudo apt install conky
mkdir -p ~/.config/conky && conky --print-config > ~/.config/conky/conky.conf
install minimalistic conky theme: https://www.gnome-look.org/p/1112273/
add conky to startup programs
bash -c "sleep 10 && conky"

# install teams
cd /tmp
wget https://packages.microsoft.com/repos/ms-teams/pool/main/t/teams/teams_1.4.00.7556_amd64.deb -O teams.deb
sudo dpkg -i teams.deb
sudo apt-get install -f

# install zoom
cd /tmp 
wget https://zoom.us/client/latest/zoom_amd64.deb
sudo dpkg -i zoom_amd64.deb
sudo apt -f install

# install teamviewer
cd /tmp 
wget https://download.teamviewer.com/download/linux/teamviewer_amd64.deb
sudo dpkg -i teamviewer_amd64.deb
sudo apt -f install

# install anydesk
wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | sudo apt-key add -
echo "deb http://deb.anydesk.com/ all main" | sudo tee /etc/apt/sources.list.d/anydesk-stable.list
sudo apt update
sudo apt install anydesk

# install etcher
echo "deb https://deb.etcher.io stable etcher" | sudo tee /etc/apt/sources.list.d/balena-etcher.list
sudo apt-key adv --keyserver hkps://keyserver.ubuntu.com:443 --recv-keys 379CE192D401AB61
sudo apt update
sudo apt install balena-etcher-electron

# install freecad
sudo add-apt-repository ppa:freecad-maintainers/freecad-stable
sudo apt-get update
sudo apt-get install freecad

# install chrome
cd /tmp
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
--- chrome extensions
https://chrome.google.com/webstore/detail/the-marvellous-suspender/noogafoofpebimajpfpamcfhoaifemoa/related?hl=en-US
https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm?hl=en-US
https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg/related?hl=en-US
https://chrome.google.com/webstore/detail/session-buddy/edacconmaakjimmfgnblocblbcdcpbko/related?hl=en-US
https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep

chrome://settings/languages
-- add spanish (latin america), portuguese (brazil)

# latex

sudo apt install -y texlive texlive-font-utils texlive-pstricks-doc texlive-base texlive-formats-extra texlive-lang-german texlive-metapost texlive-publishers texlive-bibtex-extra texlive-latex-base texlive-metapost-doc texlive-publishers-doc texlive-binaries texlive-latex-base-doc texlive-science texlive-extra-utils texlive-latex-extra texlive-science-doc texlive-fonts-extra texlive-latex-extra-doc texlive-pictures texlive-xetex texlive-fonts-extra-doc texlive-latex-recommended texlive-pictures-doc texlive-fonts-recommended texlive-humanities texlive-lang-english texlive-latex-recommended-doc texlive-fonts-recommended-doc texlive-humanities-doc texlive-luatex texlive-pstricks perl-tk cm-super
sudo apt install -y texstudio

# Microsoft Fonts
## Sometimes I get documents which require fonts from Microsoft:

sudo apt install -y ttf-mscorefonts-installer


# foxit pdf reader
cd /tmp
wget https://cdn01.foxitsoftware.com/pub/foxit/reader/desktop/linux/2.x/2.4/en_us/FoxitReader.enu.setup.2.4.4.0911.x64.run.tar.gz
tar -vzxf  FoxitReader.enu.setup.2.4.4.0911.x64.run.tar.gz
chmod +x "FoxitReader.enu.setup.2.4.4.0911(r057d814).x64.run"
./FoxitReader.enu.setup.2.4.4.0911\(r057d814\).x64.run

# install utilities
## dropbox
sudo apt install python3-gpg
cd /tmp
wget https://www.dropbox.com/download?dl=packages/ubuntu/dropbox_2020.03.04_amd64.deb
sudo dpkg -i download\?dl\=packages%2Fubuntu%2Fdropbox_2020.03.04_amd64.deb 
sudo apt-get -f install

# vpn services
sudo apt install -y openvpn network-manager-openvpn network-manager-openvpn-gnome
sudo apt-get install openconnect

# generate ssh key

ssh-keygen

# install sublime text
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt update
sudo apt-get install sublime-text

# install zsh
sudo apt install zsh
chsh -s $(which zsh)
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
sh -c "$(curl -fsSL https://git.io/zinit-install)"

-- add to the end of ~/.zshrc
zinit light zdharma/fast-syntax-highlighting
zinit light zsh-users/zsh-autosuggestions
zinit light zsh-users/zsh-completions

https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md

# install ROS
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
sudo apt update
sudo apt install ros-noetic-desktop-full
echo "source /opt/ros/noetic/setup.zsh" >> ~/.zshrc
source ~/.zshrc
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
sudo apt install python3-rosdep
sudo rosdep init
rosdep update
sudo apt-get install python3-catkin-tools



# install Spotify
curl -sS https://download.spotify.com/debian/pubkey_5E3C45D7B312C643.gpg | sudo apt-key add - 
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
sudo apt-get update && sudo apt-get install spotify-client

# fix key bindings
chrome://flags/#hardware-media-key-handling
disable

go to keyboard->customize shortcuts->play/pause
go to keyboard->customize shortcuts->next track
go to keyboard->customize shortcuts->previous track

Multimedia
VLC

The best video player:

sudo apt install -y vlc

Open it and check whether it works.
Multimedia Codecs

Install and compile multimedia codecs:

sudo apt install -y libavcodec-extra libdvd-pkg; sudo dpkg-reconfigure libdvd-pkg

OBS

Install:

    sudo apt install -y obs-studio

Open OBS and set it up, import your scenes, etc.



# Gnome 3 tweaks
- hide normal aplications in keyboard bindings, navigation
	- use super + d

sudo apt install gnome-tweaks
- windows titlebars:
    - enable minimize and maximize
- top bar:
    - enable battery percentage
    - clock show seconds

https://extensions.gnome.org/extension/1160/dash-to-panel/
-- disable window previews feature

sudo apt install gir1.2-gtop-2.0 gir1.2-nm-1.0 gir1.2-clutter-1.0 gnome-system-monitor
https://extensions.gnome.org/extension/120/system-monitor/

https://itsfoss.com/show-desktop-gnome-3/

https://extensions.gnome.org/extension/779/clipboard-indicator/
https://extensions.gnome.org/extension/602/window-list/
https://extensions.gnome.org/extension/307/dash-to-dock/

-- behaviours / click action / minimze on overview

https://extensions.gnome.org/extension/277/impatience/
	- set to 0.05

https://extensions.gnome.org/extension/1176/argos/
cp "/home/h3ct0r/Dropbox/Documents/scripts/pingtest.r.5s.sh" ~/.config/argos

https://extensions.gnome.org/extension/4167/custom-hot-corners-extended/
	- configure corner with "Show activities (overview)"

Remove dynamic workspaces
	- workspaces -> Static Workspaces -> 1

--- keyboard shortcuts
go to settings > devices > keyboard
look for the keyboard shortcut for "Switch windows"
set this to the shortcut Alt+Tab (this will overwrite the old shortcut)
settings > devices > keyboard

alt + tab to switch windows
alt + f4 to close window

-- Keyboard
US int with dead keys

--- Region and Language
settings - Region and Language - Formats - Brazil 

#### desenvolvimento
pycharm

sudo snap install clion --classic
clion

#### instalar steam
cd /tmp
wget https://repo.steampowered.com/steam/archive/precise/steam_latest.deb
sudo dpkg -i steam_latest.deb
steam


# update cuda
sudo apt install system76-cuda-latest system76-cudnn-10.2


# disable IPv6 to prevent nasty issues with ROS

https://www.reddit.com/r/pop_os/comments/jkgwbe/having_problems_with_getting_your_vpn_to_work_on/



### docker

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
