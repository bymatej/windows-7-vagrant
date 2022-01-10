# windows-7-vagrant
Windows 7 Vagrant (for games)

This is a personal project for personal use. This readme is not for everyone to read, but rather a reminder for mysefl on how I achieved certain things on this project. 

# Creating a box
## Installing Virtualbox
```
sudo apt -y install virtualbox
```

## Installing Vagrant
```
sudo apt install vagrant
```

```
vagrant plugin install vagrant-disksize
```

```
vagrant plugin install vagrant-vbguest
```

```
gem install vagrant-windows
```

```
gem install winrm
```

## Creating a virtual machine
- Download Windows 7 iso
- Creating the virtual machine in virtualbox (see details below)
  - Make sure you enable network type as NAT
- Go through the OS installation stuff
  - Create a local admin account with username/password as `vagrant/vagrant`
- Install required software (games, browsers, libraires, etc)
- Install guest additions

This is the configuration dump:
```
matej@matejs-ux303lab:~/Downloads$ vboxmanage showvminfo "Windows 7"
Name:                        Windows 7
Groups:                      /
Guest OS:                    Windows 7 (64-bit)
UUID:                        866aade4-e0a0-4f2e-be64-bdd52e485b9a
Config file:                 /home/matej/VirtualBox VMs/Windows 7/Windows 7.vbox
Snapshot folder:             /home/matej/VirtualBox VMs/Windows 7/Snapshots
Log folder:                  /home/matej/VirtualBox VMs/Windows 7/Logs
Hardware UUID:               866aade4-e0a0-4f2e-be64-bdd52e485b9a
Memory size:                 2048MB
Page Fusion:                 disabled
VRAM size:                   128MB
CPU exec cap:                100%
HPET:                        disabled
CPUProfile:                  host
Chipset:                     piix3
Firmware:                    BIOS
Number of CPUs:              2
PAE:                         disabled
Long Mode:                   enabled
Triple Fault Reset:          disabled
APIC:                        enabled
X2APIC:                      disabled
Nested VT-x/AMD-V:           disabled
CPUID Portability Level:     0
CPUID overrides:             None
Boot menu mode:              message and menu
Boot Device 1:               Floppy
Boot Device 2:               DVD
Boot Device 3:               HardDisk
Boot Device 4:               Not Assigned
ACPI:                        enabled
IOAPIC:                      enabled
BIOS APIC mode:              APIC
Time offset:                 0ms
RTC:                         local time
Hardware Virtualization:     enabled
Nested Paging:               enabled
Large Pages:                 disabled
VT-x VPID:                   enabled
VT-x Unrestricted Exec.:     enabled
Paravirt. Provider:          Default
Effective Paravirt. Prov.:   HyperV
State:                       powered off (since 2022-01-09T17:00:00.625000000)
Graphics Controller:         VBoxSVGA
Monitor count:               1
3D Acceleration:             enabled
2D Video Acceleration:       disabled
Teleporter Enabled:          disabled
Teleporter Port:             0
Teleporter Address:          
Teleporter Password:         
Tracing Enabled:             disabled
Allow Tracing to Access VM:  disabled
Tracing Configuration:       
Autostart Enabled:           disabled
Autostart Delay:             0
Default Frontend:            
VM process priority:         default
Storage Controller Name (0):            SATA
Storage Controller Type (0):            IntelAhci
Storage Controller Instance Number (0): 0
Storage Controller Max Port Count (0):  30
Storage Controller Port Count (0):      2
Storage Controller Bootable (0):        on
SATA (0, 0): /home/matej/VirtualBox VMs/Windows 7/Windows 7.vdi (UUID: c6f647d5-de64-44b5-873d-39980fb518cf)
SATA (1, 0): Empty (ejected)
NIC 1:                       MAC: 08002797BE50, Attachment: NAT, Cable connected: on, Trace: off (file: none), Type: 82540EM, Reported speed: 0 Mbps, Boot priority: 0, Promisc Policy: deny, Bandwidth group: none
NIC 1 Settings:  MTU: 0, Socket (send: 64, receive: 64), TCP Window (send:64, receive: 64)
NIC 2:                       disabled
NIC 3:                       disabled
NIC 4:                       disabled
NIC 5:                       disabled
NIC 6:                       disabled
NIC 7:                       disabled
NIC 8:                       disabled
Pointing Device:             USB Tablet
Keyboard Device:             PS/2 Keyboard
UART 1:                      disabled
UART 2:                      disabled
UART 3:                      disabled
UART 4:                      disabled
LPT 1:                       disabled
LPT 2:                       disabled
Audio:                       enabled (Driver: PulseAudio, Controller: HDA, Codec: STAC9221)
Audio playback:              enabled
Audio capture:               disabled
Clipboard Mode:              Bidirectional
Drag and drop Mode:          Bidirectional
VRDE:                        disabled
OHCI USB:                    enabled
EHCI USB:                    enabled
xHCI USB:                    disabled

USB Device Filters:

<none>

Bandwidth groups:  <none>

Shared folders:<none>

Capturing:                   active
Capture audio:               not active
Capture screens:             
Capture file:                /home/matej/VirtualBox VMs/Windows 7/Windows 7.webm
Capture dimensions:          1024x768
Capture rate:                512kbps
Capture FPS:                 25kbps
Capture options:             vc_enabled=true,ac_enabled=false,ac_profile=med

Guest:

Configured memory balloon size: 0MB
```
More info: https://docs.oracle.com/en/virtualization/virtualbox/6.0/user/vboxmanage-showvminfo.html

## Post installation stuff
- Install guest additions in the Guest OS
- Disable mouse integration
- Set correct resolution
- Install ZeroTier (check if this is necessary on guest or on host machine)
- Install required software for Vagrant box to work: http://kamalim.github.io/blogs/how-to-create-you-own-vagrant-base-boxes/ 

If you haven't already, create a local admin account with username/password as `vagrant/vagrant` (set password to not expire and uncheck must change at next login).

Required software to install (via CMD in Windows guest OS):
- winrm
```
winrm quickconfig -q
```

```
winrm set winrm/config/winrs @{MaxMemoryPerShellMB="512"}
```

```
winrm set winrm/config @{MaxTimeoutms="1800000"}
```

```
winrm set winrm/config/service @{AllowUnencrypted="true"}
```

```
winrm set winrm/config/service/auth @{Basic="true"}
```

Disable the following services:
- `UAC` (this is "User Account Control" - type UAC in windows explorer (start search), or disable it when it prompts by sliding it down to "Never notify")
- `Complex passwords` (from start menu search: gpedit.msc; Computer Configuration > windows settings > security settings > Password Policy > Password Must Meet Complexity Requirement > Disabled) (you will not have this option if this is not a domain computer)

Remove all unnecessary files and installations, perform a Disk Cleanup, and Disk defragment. 

Download SDelete and fill the blank disk space with zeroes: 
- SDelete: https://docs.microsoft.com/en-us/sysinternals/downloads/sdelete 
- in cmd perform `sdelete C: -z`

Turn off your virtual machine once you're satisfied with it

# Upload the box to Vagrant
## List all VMs and found which one is yours
```
vboxmanage list vms
```

The result should be something like this:
```
"Windows 7" {866aade4-e0a0-4f2e-be64-bdd52e485b9a}
```

## Create a box
```
vagrant init
```

```
vagrant package --base "Windows 7" --output windows7.box
```

This will generate a `windows7.box` file.

## Generate SHA hash for your box file
- https://www.a2hosting.com/kb/developer-corner/linux/working-with-file-checksums 

```
sha512sum windows7.box
```

Hash will be in the output. Copy it.

## Upload the box file to Vagrant
- Register to Vagrant
- Create a box in their user interface
- Create a version
- Set the provider (virtualbox in my case)
- Fill the upload form

More details: 
- https://www.vagrantup.com/docs/providers/virtualbox/boxes
- https://www.vagrantup.com/docs/cli/upload
- https://mudongliang.github.io/2018/06/25/create-vagrant-base-box.html
- http://kamalim.github.io/blogs/how-to-create-you-own-vagrant-base-boxes/

# Troubleshooting

## Issues on `vagrant up` with virtualbox provider
In case of vagrant-up issue that says "If your system is using EFI Secure Boot you may need to sign the kernel modules (vboxdrv, vboxnetflt, vboxnetadp, vboxpci) before you can load them.", do the following:
- Disable Secure Boot in BIOS (OPTIONAL)
- Execute the following 2 commands: 
```
sudo apt install virtualbox-dkms --reinstall
```

```
sudo modprobe vboxdrv
```

Solution:
- https://askubuntu.com/questions/1322875/virtualbox-installation-problem-on-ubuntu-20-10

# Resources
- https://github.com/jeffskinnerbox/Windows-10-Vagrant-Box
- https://github.com/bymatej/windows-server-vagrant
- 
