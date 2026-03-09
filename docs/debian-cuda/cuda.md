# CUDA Toolkit Installation Guide (Debian 13)

This guide shows how to install the **NVIDIA Driver** and **CUDA Toolkit (nvcc)** on **Debian 13**.

It includes:

- Driver verification
- Kernel and DKMS checks
- CUDA installation
- Verification steps
- Troubleshooting common issues

---

# Prerequisites

You need:

- Debian 13
- NVIDIA GPU
- Internet connection
- sudo privileges

---

# Step 1 — Update the System

Always update package lists first.

```bash
sudo apt update
```

# Step 2 — Check if the System Detects the GPU

Run:
```bash
lspci | grep -i vga
```

Example output:

bash```
01:00.0 VGA compatible controller: NVIDIA Corporation Device ...
```

If you see NVIDIA, the system detects your GPU.

#Step 3 — Check NVIDIA Driver

Verify the driver is working.
```bash
nvidia-smi
```
Example output:
```bash
+--------------------------------------------------+
| NVIDIA-SMI 555.xx      Driver Version: 555.xx    |
+--------------------------------------------------+
```
If this command fails, install the driver:
```bash
sudo apt install nvidia-driver
sudo reboot
```
Then run nvidia-smi again.

#Step 4 — Check Kernel Version
```bash
uname -r
```
Example:

```bash
6.x.x-amd64
```
#Step 5 — Verify Kernel Headers

Check installed headers:
```bash
dpkg -l | grep linux-headers
```
Verify headers match your kernel:
```bash
dpkg -l | grep linux-headers-$(uname -r)
```
Verify the build directory exists:
```bash
ls /lib/modules/$(uname -r)/build
```
If headers are missing:
```bash
sudo apt install linux-headers-amd64
```
Reboot if new headers were installed:
```bash
sudo reboot
```
#Step 6 — Verify DKMS

DKMS automatically builds kernel modules.

Check:
```bash
dkms status
```
Check version:
```bash
dkms --version
```
Install if missing:
```bash
sudo apt install dkms
Step 7 — Install Build Tools
```
CUDA compilation requires build tools.

Check:
```bash
dpkg -l | grep build-essential
```
Install if missing:
```bash
sudo apt install build-essential
Step 8 — Install Firmware
```
Check firmware packages:
```bash
dpkg -l | grep firmware
```
Install recommended firmware:
```bash
sudo apt install firmware-misc-nonfree
Step 9 — Verify NVIDIA Kernel Modules
```
Check if NVIDIA modules are loaded:
```bash
lsmod | grep nvidia
```
Expected modules:
```bash
nvidia
nvidia_uvm
nvidia_drm
nvidia_modeset
```
Check driver binding:
```bash
lspci -nnk | grep -A3 -i nvidia
```
Check kernel messages:
```bash
sudo dmesg | grep -i nvidia
```
#Step 10 — Disable Nouveau Driver (Optional- don't do it)

The open-source nouveau driver conflicts with NVIDIA.

Check:
```bash
lsmod | grep nouveau
```
If you see output, disable it.

Create a blacklist file:
```bash
sudo nano /etc/modprobe.d/blacklist-nouveau.conf
```
Add:
```bash
blacklist nouveau
options nouveau modeset=0
```
Update initramfs:
```bash
sudo update-initramfs -u
```
Reboot:
```bash
sudo reboot
```
#Step 11 — Install CUDA Toolkit

Install CUDA from Debian repositories.
```bash
sudo apt update
sudo apt install nvidia-cuda-toolkit
```
This installs:

CUDA libraries

CUDA runtime

CUDA compiler (nvcc)

CUDA development tools

#Step 12 — Verify CUDA Installation

Check CUDA compiler:
```bash
nvcc --version
```
Example output:
```bash
nvcc: NVIDIA (R) Cuda compiler driver
Cuda compilation tools, release XX.X
```
Check binary location:
```bash
which nvcc
```
Expected:
```bash
/usr/bin/nvcc
```
#Step 13 — Reboot
```bash
sudo reboot
```
#Step 14 — Final Verification

Check GPU:
```bash
nvidia-smi
```
Check CUDA:
```bash
nvcc --version
```
Check modules:
```bash
lsmod | grep nvidia
```
