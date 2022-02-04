### ThinkPad OS

#### X250
OSX 14.x https://github.com/qwerty12/X250-Hackintosh
OSX 15.x https://github.com/teddytaod/mac-catalina-thinkpad-x250
Debian/WiFi https://wiki.debian.org/iwlwifi#Installation 
`/sbin/modprobe`

```
apt install connman
connmanctl> enable wifi
connmanctl> scan wifi 
Scan completed for wifi
connmanctl> services 
$SSID    wifi_XXX_managed_psk
connmanctl> agent on
Agent registered
connmanctl> connect wifi_XXX_managed_psk
Passphrase? $PASS
Connected wifi_XXX_managed_psk
connmanctl> quit
```
settings saved in `/var/lib/connman`


#### X230
15.x https://github.com/littlegtplr/Hackintosh-X230-macOS
