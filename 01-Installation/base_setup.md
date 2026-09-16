# Arch Linux Installation: Pre-Installation Guide

Primary reference: [Arch Linux Installation Guide](https://wiki.archlinux.org/title/Installation_guide)

---

## 1. Configure Keyboard Layouts and Console Fonts

### Keyboard Layouts
* `localectl list-keymaps`: List all available keyboard keymaps.
* `loadkeys us`: Set the active keymap to a specific region (e.g., US).

### Console Fonts
* **Font Directory:** `/usr/share/kbd/consolefonts/`
* `setfont ter-132b`: Apply a specific console font to the live TTY.

---

## 2. Verify Boot Mode

* **Command:** `cat /sys/firmware/efi/fw_platform_size`

### What is Firmware?
Firmware is low-level software permanently programmed into a hardware chip's non-volatile memory (EEPROM/Flash). It bridges raw hardware and higher-level software, initializing components during power-on (POST) and providing hardware abstraction. UEFI/BIOS is classic motherboard firmware.

* **Without firmware:** The CPU cannot initialize RAM, detect storage drives, or execute a bootloader. A bad flash can "brick" hardware.
* **Without an OS:** Your computer turns on and sits at a UEFI/BIOS prompt, unable to run applications, browse the web, or manage files.

> **Analogy:** Think of firmware as a building's concrete foundation and structural blueprint; the operating system and applications are the interior rooms and furniture. You need the foundation first, and you need both for a complete system.

---

## 3. Connect to the Internet

* `ip link`: List all available network interfaces.
* `ping google.com`: Test live internet connectivity and packet transmission.

Reference: [ip-link man page](https://man.archlinux.org/man/ip-link.8)

---

## 4. Update the System Clock

The live environment requires an accurate system clock to prevent package signature verification failures and TLS certificate errors during installation. The `systemd-timesyncd` service handles time synchronization automatically once an internet connection is established.

Reference: [timedatectl man page](https://man.archlinux.org/man/timedatectl.1)

* `timedatectl set-timezone [TIMEZONE]`: Set your local system timezone.
* `timedatectl status`: Verify current time synchronization and zone settings.

## 5. Partitioning Formatting and Mounting

[PartitioningFormatting&Mounting](PartitioningFormatting&Mounting.md)