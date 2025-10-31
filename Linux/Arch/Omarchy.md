# Omarchy

- After a `reboot` into arch, simply use the following command to install Omarchy:
	```
	curl -fsSL omarchy.com/install.sh | bash
	```

## Post-Installation Steps

Things to do after installing Arch/Omarchy:

---

### Disable auto-login (if enabled)

Use sddm configuration to disable auto-login:

```
sudo nano /etc/sddm.conf.d/autologin.conf
```

Remove or comment out the following lines:

```
[Autologin]
User=
Session=
```

Then restart sddm:

```
sudo systemctl restart sddm
```

---

### Share files between Windows and Linux on local network

To share files between Windows and Linux on a local network, you can use Samba. Here’s how to set it up:
- Install Samba and create a Shared folder:
```
sudo pacman -S samba

mkdir ~/Shared
chmod 777 ~/Shared
```

- Configure Samba by editing the smb.conf file:
```
sudo nano /etc/samba/smb.conf
```
Add the following lines at the end of the file:
```
[Shared]
	path = /home/yourusername/Shared
	browseable = yes
	read only = no
	guest ok = yes
	create mask = 0777
	directory mask = 0777
	valid users = yourusername
```

> Optionally add this to the top as well:
```
[global]
   workgroup = WORKGROUP
   server min protocol = SMB2
   server max protocol = SMB3
   map to guest = Bad User
   security = user
```

- Validate the share configuration syntax:
```	
testparm
```

- Set a Samba password for your user:
```
sudo smbpasswd -a YOURUSER # create password
sudo smbpasswd -e YOURUSER # enable user
```

- Check firewall settings to allow Samba traffic:
```
sudo ufw status
```

- Manually allow Samba through the firewall if necessary:
```
sudo ufw allow 137/udp
sudo ufw allow 138/udp
sudo ufw allow 139/tcp
sudo ufw allow 445/tcp
sudo ufw reload
```

- Restart Samba services:
```
sudo systemctl restart smb nmb
```

- Test samba locally:
```
smbclient -L localhost -U YOURUSER
smbclient //localhost/Shared -U YOURUSER

smb: \> ls
```

- Get the Ipv4 address of your Linux machine:
```
ip addr | grep inet
```

- Access the shared folder from Windows File Explorer by entering the following in the address bar:
```
ping 192.168.1.xxx
Test-NetConnection 192.168.1.xxx -Port 445
```

---

### Hostname Access (Without IP)

> Omarchy is configured to use the system hostname by default. Find the `<hostname>` at `/etc/hostname`.

You can make Windows access \\omarchy (instead of \\192.168.1.xxx) by enabling Avahi/mDNS on Linux:
```
sudo pacman -S avahi nss-mdns
sudo systemctl enable --now avahi-daemon
sudo nano /etc/nsswitch.conf
```
Find the hosts: line and make sure it contains:
```
hosts: files mdns_minimal [NOTFOUND=return] dns myhostname
```
Now Windows 10/11 can connect to:
```
\\<hostname>.local\Shared
```