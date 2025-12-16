# ICS2025-PA tutorial
Author: dreamking60 - dreamlyboyczh@foxmail.com

## Environment Configuration
**Install Virtual Machine**
- VMWare Workstation Pro
- Ubuntu22.04 iso file
- Don't enable update with software while install ubuntu22.04 in configuration.

> Optional: Change image source  
> If you are in the mainland China, please change source to improve speed.

**Install required package**
- Install required package for future work
```bash
sudo apt-get update
sudo apt-get install build-essential man gcc-doc gdb git libreadline-dev libsdl2-dev vim
```

> Optional: Configure SSH Connection  
> ```bash
> sudo apt-get install openssh-server
> sudo systemctl start ssh
> sudo systemctl enable ssh
> ```
