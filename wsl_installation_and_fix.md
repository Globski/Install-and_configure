# WSL Installation and Fixes

### Description

This guide walks you through installing **Windows Subsystem for Linux (WSL)**, upgrading it to **WSL 2**, and fixing common issues like `0x800701bc`, which indicates a missing or outdated kernel component.

---

## Table of Contents

1. [Check WSL Version and Requirements](#1-check-wsl-version-and-requirements)
2. [Install WSL (Windows 10/11)](#2-install-wsl-windows-1011)
3. [Install a Linux Distribution](#3-install-a-linux-distribution)
4. [Fix: Error 0x800701bc – WSL 2 Kernel Update](#4-fix-error-0x800701bc--wsl-2-kernel-update)
5. [Set WSL 2 as Default](#5-set-wsl-2-as-default)
6. [Update Existing Distro to WSL 2](#6-update-existing-distro-to-wsl-2)
7. [Uninstall/Reinstall WSL (if needed)](#7-uninstallreinstall-wsl-if-needed)
8. [Verify Setup](#8-verify-setup)
9. [Notes](#9-notes)

---

## 1: Check WSL Version and Requirements

Ensure you're running a compatible version of Windows:

* Windows 10 version **2004+** (Build **19041+**) or **Windows 11**.
* WSL 2 requires **Virtual Machine Platform** and **Windows Subsystem for Linux** features enabled.

### Check Windows version:

```powershell
winver
```

---

## 2: Install WSL (Windows 10/11)

Open **PowerShell as Administrator** and run:

```powershell
wsl --install
```

This command installs:

* WSL 2
* The default Linux distribution (usually Ubuntu)

If `wsl --install` doesn’t work, use the manual method:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

---

## 3: Install a Linux Distribution

To list available distros:

```powershell
wsl --list --online
```

Install one (e.g., Ubuntu):

```powershell
wsl --install -d Ubuntu
```

---

## 4: Fix: Error `0x800701bc` – WSL 2 Kernel Update

This error means your WSL 2 kernel is outdated or missing.

### ✅ Fix it by downloading the WSL 2 kernel update:

1. Visit: [https://aka.ms/wsl2kernel](https://aka.ms/wsl2kernel)
2. Download and run the **`wsl_update_x64.msi`** installer.

After installation, restart your PC or run:

```powershell
wsl --shutdown
```

---

## 5: Set WSL 2 as Default

To make WSL 2 the default for all future Linux distros:

```powershell
wsl --set-default-version 2
```

---

## 6: Update Existing Distro to WSL 2

Check installed distributions:

```powershell
wsl --list --verbose
```

Convert a distro to WSL 2:

```powershell
wsl --set-version <DistroName> 2
```

Example:

```powershell
wsl --set-version Ubuntu 2
```

---

## 7: Uninstall/Reinstall WSL (if needed)

To reset or reinstall WSL components:

```powershell
wsl --unregister <DistroName>
```

Or to remove WSL components:

* Open “Add or Remove Programs”
* Uninstall “Windows Subsystem for Linux Update”
* Reinstall from [https://aka.ms/wsl2kernel](https://aka.ms/wsl2kernel)

---

## 8: Verify Setup

Check WSL status:

```powershell
wsl --status
```

Expected output should show:

* Default version: 2
* Kernel version: (e.g., 5.x.x)

---

## 9: Notes

* 💡 **WSL logs and errors**: If a distro won't launch, run it from PowerShell to capture the error.
* 🧱 If using WSL on a VM or managed device, check if **Hyper-V** and **Virtual Machine Platform** are allowed/enabled.
* 🐧 Use `wsl --update` to manually update WSL if available.
