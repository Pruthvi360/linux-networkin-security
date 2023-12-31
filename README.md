# linux-networking-security
# Networking in Different Linux distribution
```
systemctl --now disable networking
systemctl --now enable networking
systemctl start networking
```
# Debian
![image](https://github.com/Pruthvi360/linux-networkin-security/assets/107435692/00b5d1b7-e7ec-456d-85eb-6c6edcb9e18d)
```
Note:
debian 11 server = use systemctl status networking
debian 12 server = use systemctl status systemcd-networkd
debian desktop = use NetworkManager instead of networking or systemcd-networkd services
Network configuration files = /etc/network/interfaces
```
**nano /etc/network/interfaces**
```
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug enp1s0
iface enp1s0 inet static
    address 10.0.2.51/24
    gateway 10.0.2.1
```
```
ifdown <interface> and ifup <interface>
ifdown enp1s0 && ifup enp1s0
```

# Ubuntu
```
systemctl --now disable systemcd-networkd
systemctl --now enable systemcd-networkd
systemctl start systemcd-networkd
```
![image](https://github.com/Pruthvi360/linux-networkin-security/assets/107435692/6f47a18a-e660-437c-b328-6ab1b83b02f2)

```
Note:
ubuntu 22.04 server = use systemctl status systemcd-networkd
ubuntu desktop = use NetworkManager instead of networking or systemcd-networkd services
Network configuration files = /etc/netplan
```
**vim /etc/netplan/00-installer-config.yaml**
```
network:       
  version: 2
  renderer: networkd
  ethernets:
    enp1s0:
      addresses: [10.0.2.53/24]
      gateway4: 10.0.2.1
      nameservers: 
        search: [example.com]
        addresses: [10.0.2.1]
```
```
netplan try
netplan apply
```

# Fedora
```
systemctl status NetworkManager
```

<img width="481" alt="image" src="https://github.com/Pruthvi360/linux-networkin-security/assets/107435692/8a388a92-6603-47b4-89b2-f3e6d0ad67fc">


# SUSE


<img width="491" alt="image" src="https://github.com/Pruthvi360/linux-networkin-security/assets/107435692/1d4e09ef-ac65-417c-9068-54865fbb21f2">


# Other methods of network config editor
```
nmtui
nm-connection-editor
nmcli
cockpit.socket  ---> Browser based
sudo apt install cockpit && systemctl --now enable cockpit.socket && firefox https://127.0.0.1:9090
```

# Other methods of network configuration files

```
cd /etc/sysconfig/network-scripts
cd /etc/NetworkManager/system-connetions/
vim 'Wired connection 1'

```
