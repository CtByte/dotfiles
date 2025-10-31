# Installing Arch Linux

- Boot from the Arch Linux installation media (USB/DVD).
- Connect to the internet:
	- For wired connections, you should be connected automatically.
	- For wireless connections, use `iwctl`:
	```
	systemctl start iwd
	iwctl
	station list # wlan0 is typical
	station wlan0 scan
	station wlan0 get-networks
	station wlan0 connect {SSID}
	exit
	```
	- Check if connected with `ping archlinux.org`. The device can also be checked like this:
	```
	ip a  # to check network interfaces
	```
- Start the guided installer:
	```
	archinstall
	```
    - > disk configuration => partition => use a best-effort default partition layout => select disk => btrfs (Omarchy) / ext4
    - > Hostname => set your desired hostname
	- > root password => set a strong root password
	- > User account => create a user account with a strong password
	- > audio => enable audio support (pipewire)
	- > network configuration => copy ISO network configuration to install