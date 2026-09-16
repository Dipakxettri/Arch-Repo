# Quick-Ref: BIOS vs. UEFI & 32-bit vs. 64-bit

## 1. BIOS vs. UEFI (Firmware & Boot Handoff)
* **What**: Permanent firmware stored on motherboard SPI flash EEPROM. Runs POST (Power-On Self-Test) on power.

| Feature | BIOS (Legacy) | UEFI (Modern) |
| :--- | :--- | :--- |
| **Execution Mode** | 16-bit x86 Real Mode | Native 32/64-bit protected/long mode |
| **Partition Table** | MBR (Master Boot Record) | GPT (GUID Partition Table) |
| **Max Disk Size** | 2 TB hard limit | > 9 Zettabytes theoretical |
| **Boot File Target** | First 512 bytes of disk (boot sector) | `.efi` binaries inside ESP (`vfat` partition) |
| **Security / Features** | None | Secure Boot (crypto signature check), shell, UEFI network stack |

* **The Boot Handoff Flow**:
  1. Firmware initializes hardware.
  2. Scans partition table (MBR or GPT/ESP).
  3. Locates bootloader payload (`grubx64.efi`, `systemd-boot`, etc.), loads it into RAM.
  4. Jumps execution to bootloader entry point $\rightarrow$ firmware steps out.

---

## 2. 32-bit vs. 64-bit Architecture
* **Definition**: The bit-width of CPU general-purpose registers and memory address bus width per clock cycle.

| Metric | 32-bit (`x86` / `i386`) | 64-bit (`x86_64` / `amd64`) |
| :--- | :--- | :--- |
| **Register Width** | 32 bits wide chunks | 64 bits wide chunks |
| **Max Addressable RAM** | $2^{32}$ bytes = **4 GB hard ceiling** | $2^{64}$ bytes = **16 Exabytes theoretical** |
| **Pointer Size** | 4-byte memory addresses | 8-byte memory addresses |
| **Ecosystem Status** | Obsolete for general computing | Standard for all modern desktops/servers |

* **Why it matters**: 
  * A 32-bit pointer cannot store a memory address higher than `0xFFFFFFFF` (~4GB offset). Physical RAM above 4GB requires PAE hacks.
  * 64-bit processes deal with massive memory-mapped files, larger encryption register space, and native quad-word integer math in single cycles.