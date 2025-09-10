# Orphaned Packages in Arch Linux

An **orphaned package** is a package installed as a dependency for some other package, but now no installed package needs it anymore.  
These packages are safe to remove because nothing depends on them.  
They often remain on the system after uninstalling software that required them.

## Example Scenario

A user installs a package and then uninstalls that same package later. Now, if the dependencies that were installed during that package installation are not needed by any other installed package, they are **orphaned**.

## How to Check for Orphaned Packages

**List all orphaned packages:**
`pacman -Qdt`  
- `-Q` → query installed packages  
- `-d` → show packages installed as dependencies  
- `-t` → only those that are no longer needed  

**For a clean list of names only:**
`pacman -Qdtq`

## How to Remove Orphaned Packages

To safely remove all orphaned packages:  
`sudo pacman -Rns $(pacman -Qdtq)`  

**Flags:**  
- `-R` → remove package  
- `-s` → remove dependencies that are no longer needed  
- `-n` → remove configuration files  

This cleans your system of unused packages and keeps it tidy.

## When to Be Careful

- Occasionally, some orphaned packages may be useful manually even if no package depends on them.  
- Always double-check before removing if you installed something intentionally as a library or utility.

## Tip for Beginners

- Run `pacman -Qdtq` first to see what will be removed.  
- Only run the remove command if you are sure these packages are not needed.
