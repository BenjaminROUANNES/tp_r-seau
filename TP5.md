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
[benjam1@localhost ~]$ ip a

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:17:82:4d brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86180sec preferred_lft 86180sec
    inet6 fe80::a00:27ff:fe17:824d/64 scope link
       valid_lft forever preferred_lft forever
```