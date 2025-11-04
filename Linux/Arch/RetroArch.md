# Setting up RetroArch on Arch Linux

[Official documentation](https://wiki.archlinux.org/title/RetroArch)

---

## Installation

```
sudo pacman -S retroarch retroarch-assets-glui retroarch-assets-ozone retroarch-assets-xmb
```

## Enable the "Core Downloader" menu item
- Settings
- User Interface
- Menu Item Visibility
- Show "Core Downloader" => ON

## Change where the cores are saved
- Settings
- Directory
- Cores => /home/user/.config/retroarch/cores
- Core Info => /home/user/.config/retroarch/cores/info

## Download cores
- Main Menu
- Online Updater
- Core Downloader
    - NES Famicom (Nestopia)
    - NES Famicom (Mesen)