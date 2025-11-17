# Setting up Waybar on Arch Linux

[Official documentation](https://github.com/Alexays/Waybar/wiki)

---

## Config files

The config file are at `/home/user/.config/waybar/`

- style => `/home/user/.config/waybar/style.css`
- config => `/home/user/.config/waybar/config.jsonc`

Restart the waybar

```
pkill waybar && hyprctl dispatch exec waybar
```

<img src="assets/image.png">