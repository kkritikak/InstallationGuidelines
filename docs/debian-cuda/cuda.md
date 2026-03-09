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

lspci | grep -i vga

Example output:

01:00.0 VGA compatible controller: NVIDIA Corporation Device ...

If you see NVIDIA, the system detects your GPU.

Step 3 — Check NVIDIA Driver

Verify the driver is working.

nvidia-smi

Example output:

+--------------------------------------------------+
| NVIDIA-SMI 555.xx      Driver Version: 555.xx    |
+--------------------------------------------------+

If this command fails, install the driver:

sudo apt install nvidia-driver
sudo reboot

Then run nvidia-smi again.

Step 4 — Check Kernel Version
uname -r

Example:

6.x.x-amd64
Step 5 — Verify Kernel Headers

Check installed headers:

dpkg -l | grep linux-headers

Verify headers match your kernel:

dpkg -l | grep linux-headers-$(uname -r)

Verify the build directory exists:

ls /lib/modules/$(uname -r)/build

If headers are missing:

sudo apt install linux-headers-amd64

Reboot if new headers were installed:

sudo reboot
Step 6 — Verify DKMS

DKMS automatically builds kernel modules.

Check:

dkms status

Check version:

dkms --version

Install if missing:

sudo apt install dkms
Step 7 — Install Build Tools

CUDA compilation requires build tools.

Check:

dpkg -l | grep build-essential

Install if missing:

sudo apt install build-essential
Step 8 — Install Firmware

Check firmware packages:

dpkg -l | grep firmware

Install recommended firmware:

sudo apt install firmware-misc-nonfree
Step 9 — Verify NVIDIA Kernel Modules

Check if NVIDIA modules are loaded:

lsmod | grep nvidia

Expected modules:

nvidia
nvidia_uvm
nvidia_drm
nvidia_modeset

Check driver binding:

lspci -nnk | grep -A3 -i nvidia

Check kernel messages:

sudo dmesg | grep -i nvidia
Step 10 — Disable Nouveau Driver

The open-source nouveau driver conflicts with NVIDIA.

Check:

lsmod | grep nouveau

If you see output, disable it.

Create a blacklist file:

sudo nano /etc/modprobe.d/blacklist-nouveau.conf

Add:

blacklist nouveau
options nouveau modeset=0

Update initramfs:

sudo update-initramfs -u

Reboot:

sudo reboot
Step 11 — Install CUDA Toolkit

Install CUDA from Debian repositories.

sudo apt update
sudo apt install nvidia-cuda-toolkit

This installs:

CUDA libraries

CUDA runtime

CUDA compiler (nvcc)

CUDA development tools

Step 12 — Verify CUDA Installation

Check CUDA compiler:

nvcc --version

Example output:

nvcc: NVIDIA (R) Cuda compiler driver
Cuda compilation tools, release XX.X

Check binary location:

which nvcc

Expected:

/usr/bin/nvcc
Step 13 — Reboot
sudo reboot
Step 14 — Final Verification

Check GPU:

nvidia-smi

Check CUDA:

nvcc --version

Check modules:

lsmod | grep nvidia
