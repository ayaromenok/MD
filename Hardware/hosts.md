```
#gangut, eth0
#nvidia_drm.modeset=1 must be set in boot for AMD+NVidia GPUS works together
192.168.0.10    gt

#x250, wifi/eth0
192.168.0.12    x250
192.168.0.13    x250w

#RPi3B, printer host
192.168.0.100   rpi3b
192.168.0.101   rpi3bw

#CM3 - Compute Module 3(old I/O board)
192.168.1.110  	cm3

#RPi4 - 1GB
192.168.1.120 	rpi4w
129.168.1.121	rpi4

#CM3P - Compute Module 3+ (new I/O board)
192.168.1.130  	cm3pw
192.168.1.131  	cm3p

#Jetson Nano
192.168.1.140	jnw
192.168.1.141	jn

#Asus TinkerBoard
192.168.0.91	tbw
192.168.0.90	tb

#Nano Pi M4
192.168.1.160	m4w
192.168.1.161	m4

#Raspberry Pi 3A
192.168.1.170   rpi3a
192.168.1.170   rpi3aw

#Jetson Xavier NX
192.168.1.180   xnw
192.168.1.181   nx

#BeagleBone Blue
192.168.1.190
```

#### howto configure

##### RPi/Debian

*dhcpcd* used.
	
- `sudo apt install dhcpcd`
- `sudo nano /etc/dhcpcd.conf`:

```
#Eth0
interface eth0
static ip_address=192.168.1.121
#static ip6_address=fd51:42f8:caae:d92e::ff/64
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8

#Wireless
interface wlan0
static ip_address=192.168.1.120
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8
```

##### Ubuntu 20.04

`sudo nmtui`

##### Jetson
```
sudo vi /etc/default/networking
CONFIGURE_INTERFACES=no
```
```
sudo vi /etc/network/interfaces
auto eth0
iface eth0 inet static
  address 192.168.1.80
  netmask 255.255.255.0
  gateway 192.168.1.1
```

##### Ubuntu 18.04/Armbian

*NetPlan* used
 
 
- `sudo nano /etc/netplan/01-network-manager-all.yml`

```
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
#  renderer: networkd
  wifis:
    wlp3s0:
      dhcp4: no
      dhcp6: no
      addresses:
        - 192.168.1.20/24
      gateway4:  192.168.1.1
      nameservers:
              addresses: [192.168.1.1, 8.8.8.8, 8.8.4.4]
      access-points:
        "azanet":
          password: "HelloWorld"
  ethernets:
    enp0s25:
      dhcp4: no
      dhcp6: no
      addresses: [192.168.1.21/24, ]
      gateway4:  192.168.1.1
      nameservers:
              addresses: [192.168.1.1, 8.8.8.8, 8.8.4.4]
    wwp0s20u4i6:
      dhcp4: yes
      dhcp6: yes
```

autologin
sudo systemctl edit getty@tty1.service

[Service]
ExecStart=
ExecStart=-/sbin/agetty --noissue --autologin pi %I $TERM
Type=idle

##### Beaglebone
https://wiki.seeedstudio.com/BeagleBone_Blue/#step4-connect-to-wifi
https://github.com/beagleboard/beaglebone-blue/wiki/Setting-a-static-ip-address-in-wifi

systemctl status systemd-resolved.service
sudo systemctl disable systemd-resolved.service
sudo service systemd-resolved stop
sudo systemctl mask systemd-resolved.service
sudo systemctl daemon-reload


Connman uses systemd tmpfiles to overwrite /etc/resolv.conf, you can
edit /usr/lib/tmpfiles.d/connman_resolvconf.conf to avoid
/etc/resolv.conf be overwriten (remove +, on L+)

sudo nano /etc/resolv.conf
nameserver 192.168.1.1
nameserver 8.8.8.8
