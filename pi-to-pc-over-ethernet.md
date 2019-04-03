# Connect Raspberry Pi to PC through Ethernet

## Background

Having a ubuntu workstation with dual ethernet ports. One giga port is used for internet connection. Another one will be set to communicate with Pi. Raspberry Pi hardware model is 3B. To check the hardware version, use command `cat /proc/device-tree/model`.

## Steps

* On PC
  * set the ethernet port on the workstation, which is `enp4s0` in my case, manually in system network settings. Assign it a name, diable IPV6.
  * check the box `use this connection only for resources on its network`.
  * Save and close. 
  * Open `nm-connection-editor`, explicitly choose the correct MAC address for ethernet entry. In IPv4 tab, choose option `Shared to other computers`
  * manually set the ip `192.168.2.1`, netmask `24(or 255.255.255.0)`. Leave the gateway blank since two devices will connect directly.
  * save and close.
* On Pi
  * manually set the ip address to 192.168.2.2 in network configurations. 
  * save and reboot

Remember to enable SSH on Pi before connection. 

## Troubleshoots

### Pi login loop

Check the `session-errors` through `cat ~/.xsession-errors`. In current case the error is `lxsession` missing. Install it through `sudo apt install lxsession`.

Another possible error is Xauthority permission issue. Simply delete the `~/.Xauthority` file.


### Pi cannot connect to WIFI

Need to manually create file wlan `wpa_supplicant` file through `sudo nano /etc/wpa_supplicant/wpa_supplicant-wlan0.conf`. Add following content:

```bash
trl_interface=/run/wpa_supplicant
update_config=1
country=US

network={
        ssid="SSID"
        psk="password"
}
```

After that, edit the main `wpa_supplicant` file through `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`, add following content:

```bash
country=US
network={
        ssid="SSID"
        psk="password"
}
allow-hotplug wlan0
iface wlan0 inet dhcp
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
```

### When connecting to Pi, PC internet connections lost

To use both ethernet ports at the same time, we have to manually assign the MAC address to each hardware configuration.

