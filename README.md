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
```
