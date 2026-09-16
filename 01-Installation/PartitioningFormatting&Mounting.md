# Partitioning, Formatting, and Mounting

This guide summarizes the foundational steps for preparing a storage drive during an Arch Linux installation, detailing the purpose and execution of partitioning, formatting, and mounting.

---

## 1. Drive Identification (`lsblk`)
Before altering any storage, identifying the correct physical drive is essential.
* **`sda`**: The primary physical storage drive (SSD/HDD) targeted for the Arch Linux installation.
* **`loop0` / `sr0`**: Virtual and optical installation media (the live USB environment); these are ignored during target system setup.

---

## 2. Partitioning (`cfdisk`)
Partitioning carves the physical drive into isolated sections, establishing the partition table type and defining space boundaries.
* **Partition Table Type (`gpt`)**: Selected as the modern standard (GUID Partition Table), required for UEFI motherboards and drives of any capacity.
* **`sda1` (EFI Partition - ~512MB to 1GB, formatted as `vfat`)**: Dedicated to storing UEFI bootloaders and kernel images, allowing the motherboard firmware to discover and boot the operating system.
* **`sda2` (Root Partition - Remaining space, formatted as `ext4`)**: The primary workspace containing the operating system core, user applications, configurations, and personal data files.

---

## 3. Formatting (`mkfs`)
Formatting writes a specific file system structure onto a raw partition, enabling the operating system to organize, read, and write data.
* **`mkfs.fat -F32 /dev/sda1`**: Formats the EFI partition with the FAT32 file system, which is universally readable by UEFI motherboard firmware.
* **`mkfs.ext4 /dev/sda2`**: Formats the root partition with `ext4`, a robust and standard Linux file system designed to handle file permissions, directories, and journaling efficiently.

---

## 4. Mounting (`mount`)
Mounting attaches a formatted storage partition to a directory tree in the currently running live environment, making the physical drive accessible for data writing.
* **`mount /dev/sda2 /mnt`**: Links the root partition to the temporary `/mnt` directory so that subsequent system installations and configurations are written directly to the hard drive rather than temporary live memory.
* **`mkdir -p /mnt/boot` & `mount /dev/sda1 /mnt/boot`**: Creates and attaches the EFI partition to the `/mnt/boot` directory, ensuring bootloader files are placed in the correct location for system startup.