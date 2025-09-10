# **Arch Linux Pacman Commands Cheat Sheet**

---

### **1. Install packages**
`sudo pacman -S package_name`  
**Flags:**  
- `-S` → sync / install package

---

### **2. System update**
`sudo pacman -Syu`  
**Flags:**  
- `-S` → sync (install/update)  
- `-y` → refresh package database  
- `-u` → upgrade all packages  
**Explanation:** `-Syu` = refresh database + upgrade system

---

### **3. Search for a package**
`pacman -Ss package_name`  
**Flags:**  
- `-S` → sync  
- `-s` → search in repositories

---

### **4. Remove package**
`sudo pacman -R package_name`  
**Flags:**  
- `-R` → remove package

---

### **5. Remove package + unused dependencies**
`sudo pacman -Rs package_name`  
**Flags:**  
- `-R` → remove package  
- `-s` → remove dependencies not required by other packages

---

### **6. Check installed packages**
`pacman -Q`  
**Flags:**  
- `-Q` → query local packages
