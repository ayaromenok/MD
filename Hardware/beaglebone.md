

### Software

Flashing eMMC


```
sudo nano /boot/uEnv.txt
...
##enable BBB: eMMC Flasher:
cmdline=init=/opt/scripts/tools/eMMC/init-eMMC-flasher-v3.sh
```
When all blue LED's is ON - flashing is finished

#### Wi-Fi
[connect to WiFi ](https://wiki.seeedstudio.com/BeagleBone_Blue/#step4-connect-to-wifi)

##### Set static IP
```
connmanctl config wifi_987bf3d5d252_617a616e6574_managed_psk --ipv4 manual 192.168.1.190 255.255.255.0 192.168.1.1 --nameservers 192.168.1.1
```

#### Disable JS stuff
```
systemctl mask cloud9.service
systemctl mask gateone.service
systemctl mask bonescript.service
systemctl mask bonescript.socket
systemctl mask bonescript-autorun.service
systemctl mask avahi-daemon.service
```
#### Remove unnecessary soft

`sudo apt remove c9-core-installer  bonescript nodejs bb-node-red-installer`
remove ` /opt/cloud9`,     `/usr/local/lib/scpipts` ,`/usr/share/bone101`

#### Tome Zone
`dpkg-reconfigure tzdata`

### Hardware

#### Accessories
https://github.com/beagleboard/beaglebone-blue/wiki/Accessories
