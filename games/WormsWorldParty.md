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

## Vagrant setup
Vagrant is the service which will obtain the virtual machine that has the game in it.

- Install Vagrant by executing the following commands:  
```
```
