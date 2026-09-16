# Quick-Ref: rfkill (Radio Frequency Kill)

## 1. What is rfkill?
* A kernel subsystem and command-line tool used to **enable or disable hardware radio transmitters** (Wi-Fi, Bluetooth, GPS, NFC, WWAN).
* It controls physical/radio states, **not** logical network traffic, IP configurations, or firewalls.

## 2. Soft Blocks vs. Hard Blocks
* **Soft Block**: Controlled by software/OS. Can be instantly cleared using command-line tools.
* **Hard Block**: Controlled by a physical laptop switch, hardware function (`Fn`) key, or UEFI setting. **Software cannot override a hard block.**

## 3. Basic Commands
* **List all wireless devices and states:**
  `rfkill list`
* **Block a specific radio (e.g., Wi-Fi):**
  `rfkill block wifi`
* **Unblock a specific radio:**
  `rfkill unblock wifi`
* **Clear all software blocks:**
  `rfkill unblock all`

wiki : https://wiki.archlinux.org/title/Network_configuration/Wireless#Rfkill_caveat