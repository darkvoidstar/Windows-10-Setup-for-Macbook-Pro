# Full disk Windows 10 install for Macbook Pro 

### After booting Windows Installer and creating a windows 10 disk:

Software to download:

* Apple Bootcamp Windows Support Installer (apple hardware drivers): https://archive.org/details/WindowsSupport
* rEFInd Boot Manager (useful for enabling cpu virtualization): https://www.rodsbooks.com/refind
* Explorer++ File Manager (for configuring rEFInd): https://explorerplusplus.com/
* Privatezilla (windows setup scripts for removing microsoft bloatware and improving privacy/ security): https://github.com/builtbybel/privatezilla

***

## Apple Bootcamp drivers:

open powershell as **administrator** and run **Bootcamp.msi**

`C:\Users\...\WindowsSupport\WindowsSupport\BootCamp\Drivers\Apple\Bootcamp.msi`

Later open Apple Software Update and update Bootcamp software for system.


***

# EFI Boot setup

Download rEFInd .zip files and extract.

Mount EFI partition for configuration as **admin** run:
`mountvol B: /s`

Download Explorer++ and open as **admin**, go to B: volume
```
.
├── EFI
|   ├── Boot
|   |   └─── bootx64.efi
|   ├── Microsoft
|   |   ├─── Boot
|   |   └─── Recovery
```

Copy the following files within `your_extract_location\refind-bin\refind\` to `B:\EFI\refind`
```
refind_x64.efi
refind.conf-sample

```

rename `refind.conf-sample` to `refind.conf`


Type ```bcdedit /set "{bootmgr}" path \EFI\refind\refind_x64.efi``` to set rEFInd as the default EFI boot program. Note that "{bootmgr}" is entered as such, including both the quotes and braces ({}). 

If you like, type ```bcdedit /set "{bootmgr}" description "rEFInd description"``` to set a description (change rEFInd description as you see fit).

open ```refind.conf``` in notepad and change the following settings inside:
```
# boot straight to windows
timeout -1 

# enable virtualization (hyper-v)
enable_and_lock_vmx true 
```

***
### Windows Debloat
Download Privatezilla: https://github.com/builtbybel/privatezilla/releases

Download Community Packages: https://github.com/builtbybel/privatezilla#community-package
* Extract the package to Privatezilla installation directory (the extracted package must have the name scripts)
```
.
├── privatezilla
|   ├── scripts <---- Here
|   ├── packages
|   ├── privatezilla.exe

```

### Open privatezilla

### Select Windows 10 checkbox at the top and hit Apply Selected to run.

### Click the Scripts button at the top of the window to open community scripts.
* Disable Services
* Block Telemetry by Hosts
* Remove OneDrive
* Windows10Debloater
* Unpin Startmenu


***
# Dev Tools:

from Microsoft Store: Install ```Windows Terminal``` ```App Installer``` 

run ```winget install Microsoft.PowerToys --source winget```

run ```wsl --install -d Debian```













