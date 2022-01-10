# Windows XP / 7 / 8 / 8.1 / 10

## 1. ZeroTier setup
ZeroTier is the software that we use to simulate a LAN network. It's a kind-of-a VPN where one creates a network and others simply connect to it.  
- Download ZeroTier: https://download.zerotier.com/dist/ZeroTier%20One.msi
- Install ZeroTier
- Join the network created by Matej :)

## 2. Game setup
- Download the game
  - Main link: 
  - Mirror: https://private-downloads.bymatej.com/games/WormsWorldParty/WormsWorldParty.zip
- Extract the zip and go to `WWP` directory
- Read the `instructions_and_tips_wwp.txt` file
- Open the `WormsWorldParty` directory
- Find the `wwp.exe` file and right-click on it and go to Properties
- Set up the compatibility mode to `Windows XP` and click OK
- Double-click on the `wwp.exe` and wait for a while
- The game should start

-----

# Linux (Ubuntu 20.04)
## 1. ZeroTier setup
ZeroTier is the software that we use to simulate a LAN network. It's a kind-of-a VPN where one creates a network and others simply connect to it.  
- Open your Terminal
- Download and install zerotier by executing this command in terminal:  
```
curl -s https://install.zerotier.com | sudo bash
```
- Join the network created by Matej by executing the following command:  
```
sudo zerotier join network_id_provided_by_matej
```
\* Note: replace the  `network_id_provided_by_matej` with the actuall network ID.

## 2. Vagrant & VirtualBox installation
Vagrant is the service which will obtain the virtual machine that has the game in it. VirtualBox will be our provider that actually runs the virtual machine.

- Install VirtualBox by executing the following commands:  
```
sudo apt -y install virtualbox
```

- Install Vagrant by executing the following commands:  
```
sudo apt -y install vagrant
```

## 3. Running the VM using Vagrant
We need to create a Vagrantfile and spin up the box. I will give the examples on where you can create the Vagrantfile. You can do it in any path.  
Open your terminal and create a Vagrantfile (assuming you have `nano` installed). Execute the following commands: 
```
mkdir -p ~/games/windows/ && \
cd ~/games/windows/ && \ 
nano Vagrantfile
```
