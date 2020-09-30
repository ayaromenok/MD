```
#gangut, eth0
192.168.1.11    gt

#x250, wifi/eth0
192.168.1.20    x250w
192.168.1.21    x250

#RPi3B, printer host
192.168.1.100   rpi3bw
192.168.1.101   rpi3b

#CM3 - Compute Module 3(old I/O board)
192.168.1.110  	cm3

#RPi4 - 1GB
192.168.1.120 	rpi4w
129.168.1.121	rpi4

#CM3P - Compute Module 3+ (new I/O board)
192.168.1.130  	cm3pw
192.168.1.131  	cm3p
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
