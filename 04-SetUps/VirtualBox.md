# VirtualBox Installation Guide

This guide details the verified, safe procedure to install and configure VirtualBox on Arch Linux using DKMS host modules.

## Step 1: Check Kernel Version
Verify your current running kernel version to ensure proper alignment with DKMS and system headers.

- Command:
    `uname -r`
- Verification: The output confirms your exact active kernel flavor (e.g., 7.2.4-arch1-2).

---

## Step 2: Install VirtualBox and DKMS Host Modules
Install the core VirtualBox package along with the DKMS host modules and matching Linux headers.

- Command:
    `sudo pacman -S virtualbox virtualbox-host-dkms linux-headers`
- Verification:
    `pacman -Q virtualbox virtualbox-host-dkms`
  The command outputs the installed package versions.

---

## Step 3: Load the VirtualBox Driver Module
Load the required virtualization kernel module into memory.

- Command:
    `sudo modprobe vboxdrv`
- Verification:
    `lsmod | grep vboxdrv`
  The output must be non-empty, indicating the module is successfully active.

---

## Step 4: Grant User Permissions
Add your user account to the vboxusers group to manage and run virtual machines without needing root permissions.

- Command:
    `sudo usermod -aG vboxusers $USER`
- Important: Log out of your desktop session completely and log back in (or reboot) for this group change to apply.
- Verification:
    groups
  Ensure vboxusers appears in the output list. You can now launch VirtualBox by typing virtualbox or from your system's application menu.