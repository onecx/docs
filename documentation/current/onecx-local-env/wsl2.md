# Set up a WSL2 Distribution

Start Powershell as Administrator…​

## [](#helper-in-powershell)Helper in Powershell

Click here to view useful commands to manage the wsl 

```powershell
# List of distributions
wsl -l -v

# List of available distributions
wsl --list --online

# List installed
wsl --list

# List running
wsl --list --running

# Install specific into location
wsl --install Ubuntu-24.04 --location d:\wsl.24.04
# Result: d:\wsl.24.04\ext4.vhdx

# Start distro with specific user:
wsl --distribution Ubuntu-24.04 --user <username>

# Set default distro
wsl --set-default Ubuntu-24.04

# Set default user
wsl --manage Ubuntu-20.04_2 --set-default-user henry
```

## [](#export-import-linux-distribution)Export / Import Linux distribution

Click here to view useful commands for ex/importing a Linux distribution 

```powershell
# Terminate distribution
asl --terminate Ubuntu-24.04

# Export current distribution
wsl --export Ubuntu-24.04 d:\ubuntu-24.04.tar

# Import into new distribution
wsl --import Ubuntu-24.04_2 d:\ubuntu-24.04 d:\ubuntu-24.04.tar
# Result: s:\Ubuntu-20.04_2\ext4.vhdx

# Unregister distribution
wsl --unregister Ubuntu-20.04

# Using variables
$creation_date = Get-Date -Format "yyyy-MM-dd_HH-mm"
$export_file_name = "d:\wsl.24.04\ubuntu-24.04_$creation_date.tar"
wsl --export Ubuntu-24.04 $export_file_name
```

## [](#updateupgrade-ubuntu)Update/Upgrade Ubuntu

Click here to view useful commands for update/upgrade Ubuntu distribution 

```bash
# update package sources in /etc/apt/source.list
sudo apt update

# List of installed packages
sudo apt list --installed

# Upgrade packages
sudo apt upgrade -y
```

## [](#installing-linux-tools)Installing Linux Tools

* Start Terminal with distribution
* Check profiles in wsl settings  
   * Create specific profile for the new distribution  
   * Define/Change default profile
* Go to terminal instance and install teh following tools:

### [](#git)Git

```bash
sudo apt-get install git
```

### [](#ssh)SSH

```bash
sudo apt install keychain
# => copy or recreate key files into .ssh directory (check permissions)
# => readd the ssh keys
ssh-add ~/.ssh/id_rsa_github
ssh-add ~/.ssh/id_ed25519_gitlab
```

### [](#docker)Docker

```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl status docker

# Check:
sudo service docker status
docker context inspect --format '{{ .Endpoints.docker.Host }}'
#  => unix:///var/run/docker.sock
# Add user to docker group
sudo usermod -aG docker USERNAME
#  => uid=1000(henry) gid=1000(henry) groups=1000(henry),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users),989(docker)
```

### [](#jq)jq

```bash
sudo apt-get install jq
```

### [](#atuin)atuin

Very helpful managing of shell history

```bash
curl --proto '=https' --tlsv1.2 -LsSf https://setup.atuin.sh | sh -s -- --non-interactive
```

### [](#helm)helm

```bash
sudo apt-get install curl gpg apt-transport-https --yes
curl -fsSL https://packages.buildkite.com/helm-linux/helm-debian/gpgkey | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/helm.gpg] https://packages.buildkite.com/helm-linux/helm-debian/any/ any main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

### [](#nvm)nvm

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc
nvm --version
```

### [](#node-js)node.js

```bash
nvm install --lts
nvm ls
```

### [](#npm)npm

```bash
sudo apt install npm
```

### [](#angular-cli)Angular CLI

```bash
npm install -g @angular/cli
```

### [](#nx)nx

```bash
npm add --global nx
```

### [](#powerline)powerline

```bash
sudo apt install --yes powerline
```

### [](#java)java

```bash
sudo apt install openjdk-21-jre-headless
sudo apt install openjdk-25-jre-headless
```

### [](#unzip)unzip

```bash
sudo apt install unzip
```

### [](#maven)maven

```bash
mkdir ~/utils
cd ~/utils
# ...download Maven zip archive
unzip apache-maven-3.9.15-bin.zip

# add maven to path
# => ~/bin is already in $PATH
ln -s ~/utils/apache-maven-3.9.15/bin/mvn ~/bin/mvn
```
