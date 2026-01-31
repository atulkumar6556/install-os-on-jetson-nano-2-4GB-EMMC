# install-os-on-jetson-nano-2-4GB-EMMC
  * 💾 EMMC 


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

* 🖥️ **Operating System:**  
   - Ubuntu **20.04.6 LTS** (recommended)
   - Other modern Linux distributions may work but are not officially tested.

* 🖥️ **System Requirements:**
   - Minimum 4 GB RAM  
   - Minimum 2 CPU cores  
   - At least 10 GB free disk space  
   - Internet connectivity for package installation



## 🧾 Now RUN these command on linux system ( ensure you are connected internet  🌐 )- 

1. ```sudo apt-get update -y```  

2. ```sudo apt upgrade -y```

3. ```sudo mkdir sources_nano```
  
4. ```cd sources_nano```
   

 ## 💻 open browser and hit the given url (on linux )-
 -----------------------------------------------------------------------------------------------------------------

    https://developer.nvidia.com/embedded/l4t/r32_release_v7.2/t210/jetson-210_linux_r32.7.2_aarch64.tbz2


    https://developer.nvidia.com/embedded/l4t/r32_release_v7.2/t210/tegra_linux_sample-root-filesystem_r32.7.2_aarch64.tbz2
    
-------------------------------------------------------------------------------------------------------------------
📁 Move the Jetpack to a folder and extract it 

5. ```sudo mv ~/Downloads/Jetson-210_Linux_R32.7.2_aarch64.tbz2 ~/sources_nano/```

6. ```sudo mv ~/Downloads/Tegra_Linux_Sample-Root-Filesystem-R32.7.2_aarch64.tbz2 ~/sources_nano/```

📚 Unzip resource

7. ```sudo tar -xjf Jetson-210_Linux_R32.7.2_aarch64.tbz2```

8. ```cd Linux_for_Tegra/rootfs/```
9. ```sudo tar -xjf ../../Tegra_Linux_Sample-Root-Filesystem_R32.7.2_aarch64.tbz2```
10. ```cd ../```
11. ```sudo ./apply_binaries.sh```
12. ```cd ..```
13. ```wget https://developer.nvidia.com/downloads/embedded/L4T/r32_Release_v7.5/overlay_32.7.5_PCN211181.tbz2```
14. ```sudo tar -xjf overlay_32.7.5_PCN211181.tbz2```

🛠️ After this prepare your jetson nano and boot into recovery mode - 

1. Short-connect the **FC REC** and **GND** pins with a jump cap or DuPont wire, located below the core board, as shown below.
2. Connect the **DC power supply** to the round power supply port and wait a while.
3. Connect the Jetson Nano's **Micro USB port** to the Ubuntu host ( LINUX SYSTEM ) with a USB cable (note that it is a data cable).
4. After entering **recovery mode** run the given command on **terminal** into host linux system -

* ```cd ~/sources_nano/Linux_for_Tegra```
* ```sudo ./flash.sh jetson-nano-emmc mmcblk0p1```

📀 After successful flashing remove all the jumper cap/wire and reboot the jetson nano by unplug the power supply . 

# After sucessful boot and user setup 

run 

```sudo dtc -I dtb -O dts -o /tmp/nano.dts /boot/kernel_tegra210-p3448-0002-p3449-0000-b00.dtb```

```sudo cp /boot/kernel_tegra210-p3448-0002-p3449-0000-b00.dtb /boot/kernel_tegra210-p3448-0002-p3449-0000-b00_backup2.dtb```

```sudo nano /tmp/nano.dts```

search change all these -

status = "disabled";  to 

```status = "okay";```

- similarly search all given below and change as shown above status="okay"
 
sdhci@700b0200
sdhci@700b0600

sdhci@700b0400   - in this change status=okay and add more line

``` cd-gpios = <0x5b 0xc2 0x8>; ```
```   sd-uhs-sdr104; ```
```   sd-uhs-sdr50; ```
```   sd-uhs-sdr25;```
```   sd-uhs-sdr12;```

vmmc-supply = <8x4c>:  below this add this line

```no-mmc;```

```sudo dtc -I dts -O dtb -o /tmp/new_kernel.dtb /tmp/nano.dts```

```sudo cp /tmp/new_kernel.dtb /boot/kernel_tegra210-p3448-0002-p3449-0000-b00.dtb```

```sudo nano /boot/extlinux/extlinux.conf```

add one line below 

LINUX /boot/Image

```FDT /boot/kernel_tegra210-p3448-0002-p3449-0000-b00.dtb```

reboot the device 

sudo reboot

After reboot check -

```lsblk```

you will get

```
NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0          7:0    0    16M  1 loop
mmcblk0      179:0    0  14.7G  0 disk
├─mmcblk0p1  179:1    0    14G  0 part /
├─mmcblk0p2  179:2    0     1M  0 part
├─mmcblk0p3  179:3    0     6M  0 part
├─mmcblk0p4  179:4    0    80K  0 part
├─mmcblk0p5  179:5    0    64M  0 part
├─mmcblk0p6  179:6    0     1M  0 part
├─mmcblk0p7  179:7    0     6M  0 part
├─mmcblk0p8  179:8    0    80K  0 part
├─mmcblk0p9  179:9    0    64M  0 part
├─mmcblk0p10 179:10   0   192K  0 part
├─mmcblk0p11 179:11   0   256K  0 part
├─mmcblk0p12 179:12   0    63M  0 part
├─mmcblk0p13 179:13   0   512K  0 part
├─mmcblk0p14 179:14   0   256K  0 part
├─mmcblk0p15 179:15   0   256K  0 part
├─mmcblk0p16 179:16   0   300M  0 part
└─mmcblk0p17 179:17   0 185.4M  0 part
mmcblk0boot0 179:32   0     4M  1 disk
mmcblk0boot1 179:64   0     4M  1 disk
mmcblk0rpmb  179:96   0     4M  0 disk
mmcblk1      179:128  0  59.7G  0 disk
└─mmcblk1p1  179:129  0  59.7G  0 part /mnt/sdcard
zram0        252:0    0 494.5M  0 disk [SWAP]
zram1        252:1    0 494.5M  0 disk [SWAP]
zram2        252:2    0 494.5M  0 disk [SWAP]
zram3        252:3    0 494.5M  0 disk [SWAP]
```
