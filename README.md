# install-os-on-jetson-nano-2-4GB-EMMC
  * EMMC

## 🧩 Overview

This guide is designed to help you **install OS and set up Ubuntu 20.04.6 LTS** on the **NVIDIA Jetson Nano** (both 2GB and 4GB variants).  

The installation process prepares your Jetson Nano for use as a **Linux-based development platform**, suitable for AI, computer vision, robotics, and edge computing applications.  

It covers:
- Flashing OS onto a internal memory EMMC  
- Initial setup and configuration steps  
- Basic system optimization and post-installation updates  

This setup ensures a **stable and fully functional Ubuntu environment** specifically optimized for the Jetson Nano hardware.



## ⚙️ Prerequisites

Before you begin, ensure you have the following environment ready:

* =) **Operating System:**  
   - Ubuntu **20.04.6 LTS** (recommended)
   - Other modern Linux distributions may work but are not officially tested.

* =) **System Requirements:**
   - Minimum 4 GB RAM  
   - Minimum 2 CPU cores  
   - At least 10 GB free disk space  
   - Internet connectivity for package installation

* =) **Required Packages:**


1. ```sudo apt-get update -y```  

2. ```sudo apt upgrade -y```

3. ```sudo mkdir sources_nano```
  
4. ```cd sources_nano```
   

 ## 💻 open browser and hit the given url (on jetson nano )-
 -----------------------------------------------------------------------------------------------------------------

    https://developer.nvidia.com/embedded/l4t/r32_release_v7.2/t210/jetson-210_linux_r32.7.2_aarch64.tbz2


    https://developer.nvidia.com/embedded/l4t/r32_release_v7.2/t210/tegra_linux_sample-root-filesystem_r32.7.2_aarch64.tbz2
    
-------------------------------------------------------------------------------------------------------------------
Move the Jetpack to a folder and extract it 

5. ```sudo mv ~/Downloads/Jetson-210_Linux_R32.7.2_aarch64.tbz2 ~/sources_nano/```

6. ```sudo mv ~/Downloads/Tegra_Linux_Sample-Root-Filesystem-R32.7.2_aarch64.tbz2 ~/sources_nano/```

Unzip resource

7. ```sudo tar -xjf Jetson-210_Linux_R32.7.2_aarch64.tbz2```

8. ```cd Linux_for_Tegra/rootfs/```
9. ```sudo tar -xjf ../../Tegra_Linux_Sample-Root-Filesystem_R32.7.2_aarch64.tbz2```
10. ```cd ../```
11. ```sudo ./apply_binaries.sh```
12. ```cd ..```
13. ```wget https://developer.nvidia.com/downloads/embedded/L4T/r32_Release_v7.5/overlay_32.7.5_PCN211181.tbz2```
14. ```sudo tar -xjf overlay_32.7.5_PCN211181.tbz2```

After this prepare your jetson nano and boot into recovery mode - 

1. Short-connect the FC REC and GND pins with a jump cap or DuPont wire, located below the core board, as shown below.
2. Connect the DC power supply to the round power supply port and wait a while.
3. Connect the Jetson Nano's Micro USB port to the Ubuntu host ( LINUX SYSTEM ) with a USB cable (note that it is a data cable).
4. After entering recovery mode run the given command on terminal into host linux system -

* ```cd ~/sources_nano/Linux_for_Tegra```
* ```sudo ./flash.sh jetson-nano-emmc mmcblk0p1```

After successful flashing remove all the jumper cap/wire and reboot the jetson nano by unplug the power supply . 

