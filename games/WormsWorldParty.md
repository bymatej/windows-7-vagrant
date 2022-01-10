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

The `nano` editor will be opened. Simply paste this text using `Ctrl + Shift + v`:  
```
Vagrant.configure("2") do |config|
  config.vm.box = "bymatej/windows-7-with-games"
  config.vm.box_version = "0.0.1"
end
```

Then hit `Ctrl + s` and then `Ctrl + x`. This will save the file content and exit the `nano` editor.  

Then execute this command to spin up the Virtual Machine:  
```
vagrant up
```

This will take up to 20 minutes (depending on your internet speed). After your VM is up and running, open your VirtualBox application and double click on your Windows 7 machine to see the GUI.


## 4. Running the game
In virtual machine, on the Desktop, you'll see the `instructions_and_tips_wwp.txt` file. Read it first.  
Then, open the `WormsWorldParty` directory, find the `wwp.exe` file and double-click on it. Wait for about 10 seconds and the game should start.

If your mouse is too fast in the game, disable the "mouse integration" in VirtualBox. Go to Input and click on Mouse integration to disable it.
