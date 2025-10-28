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

1. **Operating System:**  
   - Ubuntu **20.04.6 LTS** (recommended)
   - Other modern Linux distributions may work but are not officially tested.

2. **System Requirements:**
   - Minimum 4 GB RAM  
   - Minimum 2 CPU cores  
   - At least 10 GB free disk space  
   - Internet connectivity for package installation

3. **Required Packages:**
   ```bash
   sudo apt-get update
   
