# Config access point

We setup ur AP using the CLI
First of all we update ur PI, than we reboot

```BASH
sudo apt-get update
sudo apt-get upgrade
reboot

```

We gone install hostapd, than we want to unmask it and enabled.
When we enable it, it is gone help us to inisiate on the start up.

```BASH
sudo apt install hostapd
sudo systemctl unmask hostapd
sudo systemctl enable hostapd

```

We gone add ur dynamic host configuration

```BASH
sudo apt install dnsmasq


```

We gone use an plugin firewall to control ur interaction with debian.

```BASH
sudo DEBIAN_FRONTEND=noninteractive apt install -y netfilter-persistent iptables-persistent

```

After we gone setup an static Ip for ur DHCP server.

```BASH
interface wlan0
    static ip_address=192.168.4.1/24
    nohook wpa_supplicant 
```

We need some routing to enable multiple clients, soo inside ur routed-ap config we gone add net.ipv4.ip_forward=1.

```BASH
sudo nano /etc/sysctl.d/routed-ap.conf
net.ipv4.ip_forward=1
```

We add an nieuw firewall, for postroute.

```BASH
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

```

We need to be sure it is saved and it can run when we start up ur Pi.

```BASH
sudo netfilter-persistent save
```

Soo we can finally configure ur DHCP server.
We make first an copy of the default file and we return an empty version. Then we start the configuration.

```BASH
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
sudo nano /etc/dnsmasq.conf 


```

Inside of dnsmasq.config we define ur range and wireless infterface.

```BASH
interface=wlan0
dhcp-range=192.168.4.2,192.168.4.20,255.255.255.0,24h
domain=wlan
address=/gw.wlan/192.168.4.1


```

The last step, ur AP setup.

```BASH

interface=wlan0
ssid=SoundBoardAP
hw_mode=g
channel=7
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=123456789PiPi
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP

```

## bibliography

https://www.instructables.com/Raspberry-Pi-Web-Server-Wireless-Access-Point-WAP/
https://www.youtube.com/watch?v=qMT-0mz1lkI
https://linuxiac.com/firewalld-1-0/


