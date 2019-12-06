# dotfiles
My Ubuntu environment dotfiles and config

# Configure OS

```sh

sudo apt update

# basic system deps
sudo apt install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  gpg \
  gnupg-agent \
  software-properties-common
  
# utilities
sudo apt install -y \
  keychain \
  git

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
  unzip curl

# asdf nodejs plugin
# https://github.com/asdf-vm/asdf-nodejs
asdf plugin-add nodejs https://github.com/asdf-vm/asdf-nodejs.git
bash ~/.asdf/plugins/nodejs/bin/import-release-team-keyring

asdf install nodejs 12.13.1
asdf global nodejs 12.13.1

# asdf python plugin
# https://github.com/danhper/asdf-python
asdf plugin-add python
asdf install python 3.7.5
asdf install python 2.7.17
asdf global python 3.7.5 2.7.17

# aws cli and sam cli
sudo apt install -y awscli
pip install --user aws-sam-cli

# chromium
sudo apt install -y chromium-browser

# postman
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz
sudo tar -xzf postman.tar.gz -C /opt
rm postman.tar.gz
sudo ln -s /opt/Postman/Postman /usr/bin/postman
cp ./postman.desktop ~/.local/share/applications/

# slack
wget https://downloads.slack-edge.com/linux_releases/slack-desktop-4.1.2-amd64.deb
sudo apt install -y ./slack-desktop-*.deb
rm slack-desktop-*.deb

# vlc
sudo apt install -y vlc
```

Visual Studio Code
```sh
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
```

Spotify
```sh
# https://www.spotify.com/us/download/linux/

curl -sS https://download.spotify.com/debian/pubkey.gpg | sudo apt-key add - 
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list

sudo apt update
sudo apt install -y spotify-client
```
## Install Configuration

```sh
cd dotfiles

ln -s `pwd`/.gitconfig ~/.gitconfig
ls -s `pwd`/.bashrc ~/.bashrc
ls -s `pwd`/vscode/keybindings.json "~/.config/Code - Insiders/User/keybindings.json"
ls -s `pwd`/vscode/settings.json "~/.config/Code - Insiders/User/settings.json"
```