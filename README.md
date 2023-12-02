# linux-networkin-security
**Two good ways to modify hostnames:**
```
hostnamectl set-hostname <hostname>
vim /etc/hostname
```
**Two locations for DNS:**
```
/etc/resolv.conf
/etc/systemd/resolved.conf
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
```
# nmcli
```
nmcli connection modify enp1s0 ipv4.dns 10.0.2.3
```
