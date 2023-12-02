# linux-networking-security
```
NOTE:
1. Ubuntu desktop doesn't use systemd-networkd but it use NetworManager
2. Ubuntu server or cli use systemd-networkd
```
**Two good ways to modify hostnames:**
```
hostnamectl set-hostname <hostname>
vim /etc/hostname  ---> (requires logoff)
```
**Two locations for DNS:**
```
/etc/resolv.conf
/etc/systemd/resolved.conf
/etc/netplan
/etc/NetworkManager/system-connections
```
**Check IP Address of linux machine with interface**
```
ip -br -c a
ip a | grep inet | sort -n
ip -o -4 a | awk '{print $4}'
ip --oneline addr | column -t
```
**Ip Address Management for the Interface meant for temporary purposes use nmcli for permanent**
```
ip a add <ip_address> dev <interface>
ip a delete 10.0.2.152/24 dev enp1s0

```
# Linux Routing
```
ip r                                  ---> To check route
ip r | grep default                   ---> To check default route
ip r delete default                   ---> To delete default route
ip r add default via 10.0.2.1         ---> To add default route with gateway
ip r add 172.21.0.0/16 dev enp1s0     ---> To add route to go with specific interface
ip -br -c a ; ip r                    ---> Check IP and Route in One go
```
# DNS and Hostname
**Note: Ubuntu uses netplan for ip assignment and dns config**
```
cat /etc/resolv.conf
cat /etc/systemd/resolved.conf

 [Resolve]
 DNS=10.0.2.1
 FallbackDNS=10.0.2.2
 #Domains=
 #LLMNR=yes
 #MulticastDNS=yes
 #DNSSEC=allow-downgrade
 #DNSOverTLS=no
 #Cache=yes
 #DNSStubListener=yes
 #ReadEtcHosts=yes

nmcli connection modify enp1s0 ipv4.dns 10.0.2.3

nano /etc/hosts

10.0.2.52      debclient.example.local debclient
```
# nmcli
**Note: Ubuntu doesn't use network manager**
```
systemctl status NetworkManager
nmcli connection modify enp1s0 ipv4.dns 10.0.2.3
nmcli con show
nmcli con mod <network-interface>
nmcli con up <network-interface>
nmcli con edit <network-interface>
```
**Modify interface using nmcli**
**Note: Can assign single or multiple address**
```
nmcli connection modify "Wired connection 1" ipv4.method manual ipv4.address 10.0.2.152/24 ipv4.gateway 10.0.2.1 ipv4.dns 10.0.2.1
nmcli connection modify "Wired connection 1" ipv4.method manual ipv4.address 10.0.2.152/24,10.0.2.153/24
nmcli connection down "Wired connection 1"
nmcli connection up "Wired connection 1"
nmcli c m "Wired connection 1" ipv4.method auto
```
**Delete the ip address use "-"**
```
nmcli c m "Wired connection 1" -ipv4.address 10.0.2.153/24
```

# NMCLI interactive shell
```
nmcli connection edit "Wired connection 1"
remove ipv4.address 10.0.2.152/24
set ipv4.address 10.0.2.52/24
save
activate
quit
```
**nmcli -h and man nmcli commands for help for using nmcli**

