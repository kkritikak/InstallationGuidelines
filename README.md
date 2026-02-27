# InstallationGuidelines
Guidelines for installing hoomd, vmd, gsd-vmd plugins, azplugins, CUDA, Nvidia-driver....

# Linux GPU & Simulation Setup Guide

This repository contains installation instructions for GPU-accelerated molecular simulation tools on Linux.

The goal is to provide **clear, safe, and reproducible installation steps** for:

- CUDA (NVCC)
- HOOMD-blue
- azplugins
- VMD
- GSD-VMD plugin

---

# 📚 Installation Guides

## 1️⃣ CUDA Installation

Install the CUDA toolkit (includes `nvcc`) after the NVIDIA driver is working.

Guide includes:
- Verifying driver with `nvidia-smi`
- Installing `nvidia-cuda-toolkit`
- Verifying `nvcc`
- Fixing PATH issues

➡ See: `docs/debian-cuda/cuda-nvcc.md`
➡ See: `docs/opensuse-cuda/cuda-nvcc.md`

---

## 2️⃣ HOOMD-blue Installation

GPU-accelerated molecular dynamics engine.

Guide includes:
- Python environment setup
- Installing prerequisties via pip (recommended)
- CUDA compatibility notes
- Verifying GPU detection

➡ See: `docs/hoomd.md`

---

## 3️⃣ azplugins Installation

HOOMD extension plugin library.

Guide includes:
- Matching HOOMD version
- Installing via pip
- Building from source (if required)
- Verifying plugin load

➡ See: `docs/azplugins.md`

---

## 4️⃣ VMD Installation

Visual Molecular Dynamics software.

Guide includes:
- Installing required system libraries
- Downloading official binary
- Running VMD
- Optional CUDA acceleration
- Creating desktop launcher

➡ See: `docs/vmd/vmd.md`

---

## 5️⃣ GSD-VMD Plugin Installation

Plugin for loading `.gsd` files into VMD.

Guide includes:
- Installing GSD Python module
- Building plugin (if required)
- Configuring VMD plugin path
- Testing GSD loading

➡ See: `docs/vmd/gsd-vmd-plugin.md`

---

# 🧠 Recommended Installation Order

For a fresh system:

1. Install NVIDIA driver
2. Install CUDA toolkit
3. Install HOOMD-blue
4. Install azplugins
5. Install VMD
6. Install GSD-VMD plugin

---

# 🛠 Tested On

- Debian 13 (Trixie)
- Opensuse Leap
- Ubuntu 20.04
- NVIDIA RTX A4000
- Driver 550+
- CUDA 12.x

---

# ⚠️ Notes

- Always verify `nvidia-smi` works before installing CUDA.
- Always verify `nvcc --version` before installing HOOMD.
- Use Python virtual environments for HOOMD to avoid conflicts.
- Ensure CUDA version is compatible with your installed NVIDIA driver.

---

# 📁 Repository Structure
