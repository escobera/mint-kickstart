# Kickstart Linux Mint

This was only tested on linux mint 19.3 cinammon.

### Table of Contents
- [Kickstart Linux Mint](#kickstart-linux-mint)
    - [Table of Contents](#table-of-contents)
    - [Common Dependencies And Software](#common-dependencies-and-software)
    - [Common Tools & Drivers](#common-tools--drivers)
      - [Nvidia Driver](#nvidia-driver)
    - [Git & Github](#git--github)
      - [Install Git & Configure SSH](#install-git--configure-ssh)
    - [Theme](#theme)
      - [Fonts](#fonts)
    - [Terminal & Shell](#terminal--shell)
      - [Tilix](#tilix)
      - [ZSH](#zsh)
    - [ASDF](#asdf)
      - [Install ASDF](#install-asdf)
    - [Visual Studio Code](#visual-studio-code)
    - [Dbeaver](#dbeaver)
    - [Docker](#docker)
    - [Postgresql 12](#postgresql-12)
    - [VPN](#vpn)
    - [Useful Commands](#useful-commands)

### Common Dependencies And Software
```sh
sudo apt install curl net-tools python3-pip \
spotify-client git vim jq automake autoconf \
libreadline-dev libncurses-dev libssl-dev libyaml-dev \
libxslt-dev libffi-dev libtool unixodbc-dev unzip \
build-essential m4 libncurses5-dev libwxgtk3.0-dev libgl1-mesa-dev \
libglu1-mesa-dev libpng-dev libssh-dev xsltproc fop inotify-tools \
apt-transport-https ca-certificates software-properties-common
```

### Common Tools & Drivers
#### Nvidia Driver
* *Driver Manager > Install Recommended Driver*

If resolution is strange after restart you probably need to: 
`sudo apt remove xserver-xorg-video-fbdev`

### Git & Github
#### Install Git & Configure SSH
1. [Generate SSH Key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
2. [Add SSH Key to Github Account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

### Theme
#### Fonts
Source Code Pro
  ``` sh
  git clone --depth 1 --branch release https://github.com/adobe-fonts/source-code-pro.git ~/.fonts/adobe-fonts/source-code-pro
  fc-cache -f -v ~/.fonts/adobe-fonts/source-code-pro
  ```

### Terminal & Shell
#### Tilix
1. Install Tilix
   
  ```sh
  sudo add-apt-repository ppa:webupd8team/terminix
  sudo apt update
  sudo apt install tilix
  ``` 
  * Fix VTE Warnings

    First create the link  
  
    `sudo ln -s /etc/profile.d/vte-2.91.sh /etc/profile.d/vte.sh` 
  
    then append its sourcing to end of `.zshrc`

    ```sh
    if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
      source /etc/profile.d/vte.sh
    fi
    ```

2. Install Dracula Theme
  ```sh
  curl -o ~/.config/tilix/schemes/Dracula.json --create-dirs https://raw.githubusercontent.com/dracula/tilix/master/Dracula.json
  ```

3. Customize Tilix Appearance
  * *Preferences > Profile > Color > Color scheme > Dracula*
4. Configure Tilix Keyboard Shortcuts (Optional)
  * *Preferences > Shortcuts > Replace **`Switch to next session`** shortcut with **`Alt+Right`***
  * *Preferences > Shortcuts > Replace **`Switch to previous session`** shortcut with **`Alt+Left`***
  * *Preferences > Shortcuts > Replace **`Paste`** shortcut with **`Ctrl+V`***
  * *Preferences > Shortcuts > Replace **`Resize the terminal down`** shortcut with **`Shift+Ctrl+Down`***
  * *Preferences > Shortcuts > Replace **`Resize the terminal up`** shortcut with **`Shift+Ctrl+Up`***
  * *Preferences > Shortcuts > Replace **`Resize the terminal right`** shortcut with **`Shift+Ctrl+Right`***
  * *Preferences > Shortcuts > Replace **`Resize the terminal left`** shortcut with **`Shift+Ctrl+Left`***
5. Configure System Keyboard Shortcuts (Optional)
  * *Keyboard Shortcuts > Remove Default Action for **`Ctrl+Alt+T`***
  * *Keyboard Shortcuts > Bind **`Ctrl+Alt+T`** to Custom Shortcut for Launching Tilix*
  * *Keyboard Shortcuts > Disable Shortcut for **`Hide all normal windows`***

#### ZSH
1. Install Zsh
  * `sudo apt install zsh`
  * `chsh -s $(which zsh)`
2. [ZimFW](https://github.com/zimfw/zimfw)
  * `curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh`
6. Add git aliases to `.zshrc`
  ```sh
  alias gp="git push"
  alias gl="git pull"
  alias g="git status"
  alias gca="git commit -a"
  alias gc="git checkout" 
  ```
****
### ASDF
#### Install ASDF

1. Install by cloning and sourcing (Note that the version number may differ)
  ``` sh
  git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.7.8
  . $HOME/.asdf/asdf.sh
  ```
2. Add plugins
  ```sh
  asdf plugin add erlang
  asdf plugin add elixir
  asdf plugin add nodejs
  asdf plugin add ruby
  asdf plugin-add java https://github.com/halcyon/asdf-java.git

  # source nodejs keyring
  bash ~/.asdf/plugins/nodejs/bin/import-release-team-keyring
  ```

3. Add asdf script and completions to .zshrc
  ```sh
  echo -e "\n. $HOME/.asdf/asdf.sh" >> ~/.zshrc
  echo -e "\nfpath=(${ASDF_DIR}/completions $fpath)" >> ~/.zshrc
  echo -e "\nautoload -Uz compinit && compinit" >> ~/.zshrc
  ```

4. Install plugins (this may vary A LOT)
  ```sh
  ASDF_CONCURRENCY=4 asdf install ruby 2.6.6
  asdf global ruby 2.6.6

  asdf install erlang 22.3
  asdf global erlang 22.3

  asdf install elixir 1.10.2-otp-22
  asdf global elixir 1.10.2-otp-22

  asdf install nodejs 12.16.1
  asdf global nodejs 12.16.1

  asdf install java adopt-openjdk-13.0.2+8
  asdf global java adopt-openjdk-13.0.2+8
  echo -e "\n. $HOME/.asdf/plugins/java/set-java-home.sh" >> ~/.zshrc
  ```
****

### Visual Studio Code
1. [Download the .deb package](https://code.visualstudio.com/docs/?dv=linux64_deb) 
2. Install settings sync

### Dbeaver
1. [Download the .deb package](https://dbeaver.io/download/?start&os=linux&arch=x86_64&dist=deb)
2. Import project
   
### Docker
``` sh
# 1. remove any older versions
sudo apt purge docker lxc-docker docker-engine docker.io

# 2. install prerequisites
sudo apt install 

# 3. import official GPG key & verify signature
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add

# 4. add docker respository
sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

# 5. install docker
sudo apt update && sudo apt install docker-ce

# 6. verify service status
sudo systemctl status docker

# 7. create docker group & add your user
sudo usermod -aG docker $USER
```

> Log out and login back.

``` sh
# 8. verify that you can run this command without 'sudo'
docker run hello-world

# 9. install docker-compose 1.25.4 (better check newer versions)
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 10. apply executable permission
sudo chmod +x /usr/local/bin/docker-compose
```

### Postgresql 12
```sh
# Add the key
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Add the repo
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" > /etc/apt/sources.list.d/postgresql.list'

# Update & Install
sudo apt update
sudo apt install postgresql-12

# Create dev user
sudo su postgres
psql
> CREATE ROLE 'role_name' WITH LOGIN SUPERUSER PASSWORD 'role_password';
> \q
```

### VPN
```sh
docker run -ti --privileged --rm --net=host -v /etc/resolv.conf:/etc/resolv.conf robertbeal/openconnect:latest --protocol=gp acessoremoto.tjdft.jus.br
```

### Useful Commands
``` sh
# fix The following signatures couldn't be verified because the public key is not available: NO_PUBKEY __key__
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys __key__

# list which processes listen on which TCP ports
netstat -tlnp
```
