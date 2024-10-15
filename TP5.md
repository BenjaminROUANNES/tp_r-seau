# TP Réseau 5

## I. Setup

☀️ Uniquement avec des commandes, prouvez-que 

IP PC:
```powershell
PS C:\Users\benja> ipconfig

Configuration IP de Windows


Carte Ethernet Ethernet 2 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::dac7:3831:1f8a:e26%11
   Adresse IPv4. . . . . . . . . . . . . .: 10.5.1.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :
```

IP Client 1:

```powershell
ben@ben-ubuntu:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:bb:cc:37 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global enp0s3
       valid_lft forever preferred_lft forever
    inet 192.168.56.107/24 metric 100 brd 192.168.56.255 scope global dynamic enp0s3
       valid_lft 454sec preferred_lft 454sec
```

IP Client 2:

```powershell
ben@ben-ubuntu:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:bb:cc:37 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global enp0s3
       valid_lft forever preferred_lft forever
    inet 192.168.56.107/24 metric 100 brd 192.168.56.255 scope global dynamic enp0s3
       valid_lft 562sec preferred_lft 562sec
    inet6 fe80::a00:27ff:febb:cc37/64 scope link
       valid_lft forever preferred_lft forever
```

IP Routeur:

```powershell
[benjam1@localhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:17:82:4d brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86180sec preferred_lft 86180sec
    inet6 fe80::a00:27ff:fe17:824d/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:de:1b:b3 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fede:1bb3/64 scope link
       valid_lft forever preferred_lft forever
```

PING PC: 

```powershell
ben@ben-ubuntu:~$ ping 10.5.1.1
PING 10.5.1.1 (10.5.1.1) 56(84) bytes of data.
^C
--- 10.5.1.1 ping statistics ---
139 packets transmitted, 0 received, 100% packet loss, time 141330ms
```

PING Client 1:
```powershell
PS C:\Users\benja> ping 10.5.1.11

Envoi d’une requête 'Ping'  10.5.1.11 avec 32 octets de données :
Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.5.1.11:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

PING Client 2:
```powershell
PS C:\Users\benja> ping 10.5.1.12

Envoi d’une requête 'Ping'  10.5.1.12 avec 32 octets de données :
Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.5.1.12:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

PING Routeur:
```powershell
PS C:\Users\benja> ping 10.5.1.254

Envoi d’une requête 'Ping'  10.5.1.254 avec 32 octets de données :
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.5.1.254:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

## II. Accès internet pour tous

### 1. Accès internet routeur

☀️ Déjà, prouvez que le routeur a un accès internet

```powershell
[benjam1@localhost ~]$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=51 time=237 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=51 time=190 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=51 time=265 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=51 time=222 ms
64 bytes from 1.1.1.1: icmp_seq=5 ttl=51 time=233 ms
64 bytes from 1.1.1.1: icmp_seq=6 ttl=51 time=258 ms
64 bytes from 1.1.1.1: icmp_seq=7 ttl=51 time=46.4 ms
^C
--- 1.1.1.1 ping statistics ---
7 packets transmitted, 7 received, 0% packet loss, time 6013ms
rtt min/avg/max/mdev = 46.392/207.513/265.474/69.693 ms
```

☀️ Activez le routage

```powershell
[benjam1@localhost ~]$ sudo firewall-cmd --add-masquerade --permanent
success
[benjam1@localhost ~]$ sudo firewall-cmd --reload
success
```

☀️ Déjà, prouvez que le routeur a un accès internet

```powershell
[benjam1@localhost ~]$ ping youtube.com
PING youtube.com (142.250.179.110) 56(84) bytes of data.
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=1 ttl=113 time=47.8 ms
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=2 ttl=113 time=45.8 ms
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=3 ttl=113 time=41.9 ms
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=4 ttl=113 time=60.7 ms
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=5 ttl=113 time=56.3 ms
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=6 ttl=113 time=54.3 ms
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=7 ttl=113 time=60.7 ms
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=8 ttl=113 time=50.7 ms
^C
--- youtube.com ping statistics ---
9 packets transmitted, 9 received, 0% packet loss, time 8019ms
rtt min/avg/max/mdev = 41.871/53.885/66.835/7.622 ms
ping: write error
```

### 2. Accès internet clients

☀️ Prouvez que les clients ont un accès internet

Pour Client 1:

```powershell
ben@ben-ubuntu:~$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=50 time=56.8 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=50 time=55.2 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=50 time=53.2 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=50 time=68.4 ms
64 bytes from 1.1.1.1: icmp_seq=5 ttl=50 time=50.4 ms
64 bytes from 1.1.1.1: icmp_seq=6 ttl=50 time=49.7 ms
^C
--- 1.1.1.1 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5008ms
rtt min/avg/max/mdev = 49.650/55.599/68.373/6.227 ms
```

Pour Client 2:

```powershell
ben@ben-ubuntu:~$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=110 time=57.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=110 time=66.0 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=110 time=61.6 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=110 time=59.4 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=110 time=59.2 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=110 time=52.0 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=110 time=47.7 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=110 time=41.6 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=110 time=60.5 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=110 time=55.4 ms
^C
--- 8.8.8.8 ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 9194ms
rtt min/avg/max/mdev = 41.615/56.117/65.973/6.837 ms
```

☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau

Pour Client 1:

```powershell
ben@ben-ubuntu:~$ cat /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [10.5.1.11/24]
      gateway4: 10.5.1.254
```

Pour Client 2:

```powershell
ben@ben-ubuntu:~$ sudo cat /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
```

## III. Serveur SSH

☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH

```powershell
[benjam1@localhost ~]$ sudo ss -lnpt | grep 22
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=695,fd=3))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=695,fd=4))
```  

☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert

```powershell
[benjam1@localhost ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports:
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

## IV. Serveur DHCP

### 3. Rendu attendu

#### A. Installation et configuration du serveur DHCP

☀️ Installez et configurez un serveur DHCP sur la machine ```routeur.tp5.b1```

```powershell
[benjam1@localhost ~]$ sudo dnf -y install dhcp-server
[benjam1@localhost ~]$ sudo nano /etc/dhcp/dhcpd.conf
```

```powershell
# create new
# specify domain name
option domain-name     "srv.world";
# specify DNS server's hostname or IP address
option domain-name-servers     dlp.srv.world;
# default lease time
default-lease-time 600;
# max lease time
max-lease-time 7200;
# this DHCP server to be declared valid
authoritative;
# specify network address and subnetmask
subnet 10.5.1.0 netmask 255.255.255.0 {
    # specify the range of lease IP address
    range dynamic-bootp 10.5.1.137 10.5.1.237;
    # specify broadcast address
    option broadcast-address 10.5.1.255;
    # specify gateway
    option routers 10.5.1.254;
}
```

```powershell
[benjam1@localhost ~]$ sudo systemctl enable --now dhcpd
```

#### B. Test avec un nouveau client

☀️ Créez une nouvelle machine client ```client3.tp5.b1```

```powershell
ben@ben-ubuntu:~$ sudo hostnamectl set-hostname client3.tp5.b1 
[sudo] password for ben: 
ben@ben-ubuntu:~$ sudo hostnamectl
 Static hostname: client3.tp5.b1
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: d353da28d9e2496291923b4d9e8e60b1
         Boot ID: d7d74515f1df40b683b7fe1f324eb4e0
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS              
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w 1d
```
```powershell
ben@ben-ubuntu:~$ sudo nano /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: yes
```



#### C. Consulter le bail DHCP

☀️ Consultez le bail DHCP qui a été créé pour notre client

☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC


