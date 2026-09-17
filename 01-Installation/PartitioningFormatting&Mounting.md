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
More details : https://wiki.archlinux.org/title/EFI_system_partition

* **`sda2` (Root Partition - Remaining space, formatted as `ext4`)**: The primary workspace containing the operating system core, user applications, configurations, and personal data files.
More detail:    
https://en.wikipedia.org/wiki/Root_directory

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

## 5. Understanding and Implementing Swap

This note covers the definition of swap space, why a dedicated swap partition is optional during initial setup, and how to create a swap file post-installation.

---

### i. What is Swap?
Swap space acts as **overflow memory** when physical RAM is fully utilized:
* **Memory Protection:** Prevents system crashes or freezes by moving inactive RAM data to storage.
* **Hibernation:** Required if you want to save the system's active state to disk when powering off.

---

### ii. Why Skip a Swap Partition During Setup?
Creating a dedicated swap partition upfront is optional for modern installations:
* **Sufficient RAM:** Systems equipped with 8GB, 16GB, or more physical memory rarely exhaust capacity under normal use[cite: 2].
* **Flexibility of Swap Files:** Instead of locking down fixed partition sizes, creating a **swap file** later allows for easy resizing or deletion without modifying partition tables[cite: 2].

---

### iii. How to Create a Swap File (Post-Installation)
Once your system is installed and you have booted into your new environment, you can easily create a swap file using these commands[cite: 2]:

1. **Allocate space** (e.g., a 2GB swap file)[cite: 2]:
   ```bash
   dd if=/dev/zero of=/swapfile bs=1M count=2048 status=progress

2. **Set secure permissions (only root should read/write to it):**
`chmod 600 /swapfile`

3. **Format the file as swap:**
`mkswap /swapfile`

4.  **Enable the swap file:**
`swapon /swapfile`
5. **Make it permanent by adding this line to /etc/fstab:**
`/swapfile none swap defaults 0 0`

