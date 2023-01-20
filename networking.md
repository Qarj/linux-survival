## Check connectivity to a port

Check port reachable on a host, server port reachable, host port reachable

```
nc -zv 127.0.0.1 80
.
Connection to 127.0.0.1 80 port [tcp/*] succeeded!
.
echo $?
0
```

Timeout in 4 seconds

```sh
nc -zv unreachable.port.com 449 -w 4
.
nc: connect to unreachable.port.com port 449 (tcp) timed out: Operation now in progress
nc: connect to unreachable.port.com port 449 (tcp) timed out: Operation now in progress
nc: connect to unreachable.port.com port 449 (tcp) timed out: Operation now in progress
nc: connect to unreachable.port.com port 449 (tcp) timed out: Operation now in progress
.
echo $?
1
```

```
cat < /dev/tcp/127.0.0.1/8080
.
SSH-2.0-APACHE-SSHD-2.7.0
```

# DNS

On another machine, find the DNS server you want - first ip address of

```
nslookup my.internal.domain
```

Check what servers are currently being used by Ubuntu 20.04

```
systemd-resolve --status | grep 'DNS Servers' -A2
```

Update via config - might need to do both method 1 and method 2 together, then run this a few times.

If you do use method 2, need to update it also later when DNS server changes.

```
sudo netplan apply
sudo resolvconf -u
systemd-resolve --status | grep 'DNS Servers' -A2
```

# Method 1 netplan

```
cd /etc/netplan
ls
.
01-network-manager-all.yaml
.
sudo nano 01-network-manager-all.yaml
```

Update with your DNS servers

```
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens3:
      dhcp4: no
      nameservers:
          addresses: [8.8.8.8, 8.8.4.4]
```

```
sudo netplan apply
systemd-resolve --status | grep 'DNS Servers' -A2
```

# Method 2

```
sudo apt install resolvconf
sudo systemctl enable --now resolvconf.service
sudo gedit /etc/resolvconf/resolv.conf.d/head
```

Add to file

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

```
sudo resolvconf -u
```
