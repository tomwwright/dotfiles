# dotfiles

My Ubuntu environment dotfiles and config

## Configuration

Configure Chromium, 1Password, download SSH key

```sh

sudo apt update

# chromium
sudo apt install -y \
  chromium-browser \
  git \
  keychain \
  jq

# configure 1Password X extension and download tom.pem (and .pub) key
keychain ~/.ssh/tom.pem

# clone this repo
mkdir ~/Projects
cd ~/Projects
git clone git@github.com:tomwwright/dotfiles.git

# install dotfiles config
cd dotfiles
ln -sf `pwd`/.gitconfig ~/.gitconfig
ln -sf `pwd`/.bashrc ~/.bashrc
mkdir -p ~/.config/Code\ -\ Insiders/User/
ln -s `pwd`/vscode/keybindings.json ~/.config/Code\ -\ Insiders/User/keybindings.json
ln -s `pwd`/vscode/settings.json ~/.config/Code\ -\ Insiders/User/settings.json
```

```sh

# basic system deps
sudo apt install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  gpg \
  gnupg-agent \
  software-properties-common

# visual studio code
# https://linuxize.com/post/how-to-install-visual-studio-code-on-ubuntu-18-04/
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"

sudo apt update
sudo apt install -y code-insiders

# extensions
code-insiders --install-extension amazonwebservices.aws-toolkit-vscode
code-insiders --install-extension eamodio.gitlens
code-insiders --install-extension esbenp.prettier-vscode
code-insiders --install-extension kisstkondoros.vscode-codemetrics
code-insiders --install-extension mauve.terraform
code-insiders --install-extension mikestead.dotenv
code-insiders --install-extension ms-azuretools.vscode-docker
code-insiders --install-extension ms-python.python
code-insiders --install-extension PKief.material-icon-theme
code-insiders --install-extension redhat.vscode-yaml
code-insiders --install-extension ritwickdey.LiveServer
code-insiders --install-extension samuelcolvin.jinjahtml
code-insiders --install-extension SirTobi.pegjs-language
code-insiders --install-extension vscoss.vscode-ansible
code-insiders --install-extension hediet.vscode-drawio

# docker
# https://docs.docker.com/install/linux/docker-ce/ubuntu/
# https://stackoverflow.com/questions/45023363/what-is-docker-io-in-relation-to-docker-ce-and-docker-ee/57678382#57678382
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt install -y docker.io

sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker tom
docker --version

# docker compose
# https://docs.docker.com/compose/install/
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# asdf version manager
# https://asdf-vm.com/#/core-manage-asdf-vm?id=install-asdf-vm
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.7.5
exec bash
sudo apt install -y \
  automake autoconf libreadline-dev \
  libncurses-dev libssl-dev libyaml-dev \
  libxslt-dev libffi-dev libtool unixodbc-dev \
  unzip curl zlib1g-dev

# asdf nodejs plugin
# https://github.com/asdf-vm/asdf-nodejs
asdf plugin-add nodejs https://github.com/asdf-vm/asdf-nodejs.git
bash ~/.asdf/plugins/nodejs/bin/import-release-team-keyring

asdf install nodejs 12.13.1
asdf global nodejs 12.13.1

# packages to support Python modules
sudo apt install -y \
  libbz2-dev libsqlite3-dev

# asdf python plugin
# https://github.com/danhper/asdf-python
asdf plugin-add python
asdf install python 3.7.5
asdf install python 2.7.17
asdf global python 3.7.5 2.7.17

# aws cli and sam cli
sudo apt install -y awscli
pip install --user aws-sam-cli

# sesion manager plugin for aws cli
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb"
sudo dpkg -i session-manager-plugin.deb


# postman
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz
sudo tar -xzf postman.tar.gz -C /opt
rm postman.tar.gz
sudo ln -s /opt/Postman/Postman /usr/bin/postman
cp ./postman/postman.desktop ~/.local/share/applications/

# slack
wget https://downloads.slack-edge.com/linux_releases/slack-desktop-4.1.2-amd64.deb
sudo apt install -y ./slack-desktop-*.deb
rm slack-desktop-*.deb

# vlc
sudo apt install -y vlc

# spotify
# https://www.spotify.com/us/download/linux/

curl -sS https://download.spotify.com/debian/pubkey.gpg | sudo apt-key add -
sudo add-apt-repository "deb http://repository.spotify.com stable non-free"

sudo apt update
sudo apt install -y spotify-client

# draw.io
wget https://github.com/jgraph/drawio-desktop/releases/download/v12.9.3/draw.io-amd64-12.9.3.deb
sudo apt install ./draw.io-amd64-12.9.3.deb
rm draw.io-*.deb

# https://gnomepomodoro.org/
sudo apt install gnome-shell-pomodoro

# conky
sudo apt install conky
ln -s `pwd`/conky/.conkyrc ~/.conkyrc
ln -s `pwd`/conky/conky.desktop ~/.config/autostart/conky.desktop
```

## Mac OS

Download `tom.pem` SSH key from 1Password

```sh
# configure SSH key
mkdir ~/.ssh
cp ~/Downloads/tom.pem ~/.ssh 
chmod 0400 ~/.ssh/tom.pem
ssh-add -K ~/.ssh/tom.pem

# clone this repo
mkdir ~/Projects
cd ~/Projects
git clone git@github.com:tomwwright/dotfiles.git
```

## Oh my Zsh

```sh
# install Oh My Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# install Oh My ZSH plugins
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting

# install Starship prompt https://github.com/starship/starship
curl -fsSL https://starship.rs/install.sh | bash
```

## Homebrew

```sh
# install Homebrew https://brew.sh/
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# install global Brewfile
ln -sf `pwd`/Brewfile ~/.Brewfile
brew bundle --global
```

