This is what i was faced and may also help others.

# Fix Brave (or Chromium) Logging Out When Switching Between KDE and Hyprland

## The Problem
When switching between KDE Plasma and Hyprland on Linux, Brave loses all saved logins and session cookies. Logging back in on one environment and switching back to the other wipes everything out again, leaving you trapped in a loop of constant re-authentications.

## The Cause
Different desktop environments use different system keyrings/secret services to encrypt and store browser credentials (KDE uses KWallet, while Hyprland often lacks an active default keyring like GNOME Keyring). When Brave cannot unlock or read the expected keyring upon switching sessions, it fails to decrypt the profile files and corrupts or resets the local login state.

## The Solution
Force Brave to bypass external desktop keyrings entirely and use its own built-in internal encrypted password storage by passing a command-line flag.

### Test it out via terminal:
brave --password-store=basic

### Make it permanent:
Open your system's Brave desktop launcher configuration file:
sudo nano /usr/share/applications/brave-browser.desktop

### Update the execution lines:
Find every line starting with Exec= and append --password-store=basic to the end of them:

Exec=brave %U --password-store=basic
Exec=brave --password-store=basic
Exec=brave --incognito --password-store=basic

### Save and exit:
Press Ctrl + O, hit Enter, then press Ctrl + X.

