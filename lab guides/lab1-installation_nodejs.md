# nodejs and docker installation
We will be installing nodejs to run backstage and we will be installing nodejs version 18  
Why version 18?  
Because due to some core difference in nodejs later versions so we will need to install some other packages (build-essential) too if we want to create the backstage  
so lets start
### Step 1
becoming root 
```
sudo -i
```
### Step 2
updating package manager
```
apt update -y
```
### Step 3
installing nodejs
```
curl -fsSL https://deb.nodesource.com/setup_18.x -o nodesource_setup.sh
bash nodesource_setup.sh
apt-get install -y nodejs
```
### Step 4 
enabling corepack
```
npm install -g corepack
```
### Step 5 
installing docker 
official website : https://docs.docker.com/engine/install/ubuntu/
```
# Add Docker's official GPG key:
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
