# TP Réseaux 6

## II. LAN clients

### 2. Client

☀️ Prouvez que...

```powershell
ben@client1:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:2c:89:cd brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s3
       valid_lft 41122sec preferred_lft 41122sec
    inet6 fe80::a00:27ff:fe2c:89cd/64 scope link
       valid_lft forever preferred_lft forever
```

```powershell
ben@client1:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: none
         Protocols: -DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
```
```powershell
ben@client1:~$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=50 time=67.7 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=50 time=65.0 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=50 time=63.9 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=50 time=62.6 ms
64 bytes from 1.1.1.1: icmp_seq=5 ttl=50 time=57.6 ms

^C--- 1.1.1.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4010ms
rtt min/avg/max/mdev = 57.649/63.381/67.739/3.322 ms
```


## III. LAN serveurzzzz

### 1. Serveur Web

☀️ Déterminer sur quel port écoute le serveur NGINX

```powershell
[benjam1@web network-scripts]$ sudo ss -lnpt | grep nginx
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1722,fd=6),("nginx",pid=1721,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1722,fd=7),("nginx",pid=1721,fd=7))
```
☀️ Ouvrir ce port dans le firewall
```powershell
[benjam1@web network-scripts]$ sudo firewall-cmd --permanent --add-port=80/tcp
success
[benjam1@web network-scripts]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 80/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```
