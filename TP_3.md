# TP Réseau 3 
## I. ARP basics

☀️ Avant de continuer...

affichez l'adresse MAC de votre carte WiFi !

```powershell
PS C:\Users\benja> arp -a

Interface : 10.33.78.240 --- 0x13
  Adresse Internet      Adresse physique      Type
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.242.6.7           01-00-5e-72-06-07     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

☀️ Affichez votre table ARP

```powershell
PS C:\Users\benja> arp -a

Interface : 192.168.56.1 --- 0xa
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.242.6.7           01-00-5e-72-06-07     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 10.33.78.240 --- 0x13
  Adresse Internet      Adresse physique      Type
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.242.6.7           01-00-5e-72-06-07     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

☀️ Supprimez la ligne qui concerne la passerelle

```powershell
PS C:\WINDOWS\system32> arp -d 10.33.79.254; arp -a

Interface : 192.168.56.1 --- 0xa
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.242.6.7           01-00-5e-72-06-07     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  239.255.255.253       01-00-5e-7f-ff-fd     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 10.33.78.240 --- 0x13
  Adresse Internet      Adresse physique      Type
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.242.6.7           01-00-5e-72-06-07     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  239.255.255.253       01-00-5e-7f-ff-fd     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

☀️ Prouvez que vous avez supprimé la ligne dans la table ARP

```powershell
PS C:\WINDOWS\system32> arp -d 10.33.79.254; arp -a

Interface : 192.168.56.1 --- 0xa
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.242.6.7           01-00-5e-72-06-07     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  239.255.255.253       01-00-5e-7f-ff-fd     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 10.33.78.240 --- 0x13
  Adresse Internet      Adresse physique      Type
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.242.6.7           01-00-5e-72-06-07     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  239.255.255.253       01-00-5e-7f-ff-fd     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

☀️ Wireshark

```
1	0.000000	ce:38:75:32:40:75	Broadcast	ARP	56	ARP Announcement for 10.33.78.190

2	9.419151	RivetNetwork_05:18:db	Broadcast	ARP	42	Who has 10.33.68.254? (ARP Probe)

3	10.243803	ca:4f:d2:62:b8:e9	Broadcast	ARP	56	ARP Announcement for 10.33.72.206
```

## II. ARP dans un réseau local
### 1. Basics

☀️ Déterminer

```powershell
PS C:\Users\benja> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Realtek 8821CE Wireless LAN 802.11ac PCI-E NIC
   Adresse physique . . . . . . . . . . . : 20-0B-74-37-40-D5
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6. . . . . . . . . . . . . .: 2a0d:e487:31f:e571:81cb:92f:5dbd:fa19(préféré)
   Adresse IPv6 temporaire . . . . . . . .: 2a0d:e487:31f:e571:b1f2:75b3:dd62:f65a(préféré)
   Adresse IPv6 de liaison locale. . . . .: fe80::23e8:9aaf:d683:5bb0%19(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.176.235(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Bail obtenu. . . . . . . . . . . . . . : mardi 8 octobre 2024 15:48:07
   Bail expirant. . . . . . . . . . . . . : mardi 8 octobre 2024 16:48:12
   Passerelle par défaut. . . . . . . . . : fe80::815:b2ff:fefc:8c5f%19
                                       192.168.176.230
   Serveur DHCP . . . . . . . . . . . . . : 192.168.176.230
   IAID DHCPv6 . . . . . . . . . . . : 169872244
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2E-08-A9-A5-20-0B-74-37-40-D5
   Serveurs DNS. . .  . . . . . . . . . . : 192.168.176.230
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```

☀️ DIY

```powershell
PS C:\Users\benja> ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6. . . . . . . . . . . . . .: 2a0d:e487:31f:e571:81cb:92f:5dbd:fa19
   Adresse IPv6 temporaire . . . . . . . .: 2a0d:e487:31f:e571:60d8:ae9:192f:d3c6
   Adresse IPv6 de liaison locale. . . . .: fe80::23e8:9aaf:d683:5bb0%19
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.34.12
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . : fe80::815:b2ff:fefc:8c5f%19
```

☀️ Pingz !

```powershell
PS C:\Users\benja> ping 192.168.34.100

Envoi d’une requête 'Ping'  192.168.34.100 avec 32 octets de données :
Réponse de 192.168.34.100 : octets=32 temps=11 ms TTL=128
Réponse de 192.168.34.100 : octets=32 temps=43 ms TTL=128
Réponse de 192.168.34.100 : octets=32 temps=40 ms TTL=128
Réponse de 192.168.34.100 : octets=32 temps=42 ms TTL=128

Statistiques Ping pour 192.168.34.100:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 11ms, Maximum = 43ms, Moyenne = 34ms
PS C:\Users\benja> ping 192.168.34.20

Envoi d’une requête 'Ping'  192.168.34.20 avec 32 octets de données :
Réponse de 192.168.34.20 : octets=32 temps=190 ms TTL=128
Réponse de 192.168.34.20 : octets=32 temps=45 ms TTL=128
Réponse de 192.168.34.20 : octets=32 temps=8 ms TTL=128
Réponse de 192.168.34.20 : octets=32 temps=4 ms TTL=128

Statistiques Ping pour 192.168.34.20:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 4ms, Maximum = 190ms, Moyenne = 61ms
```

```powershell
PS C:\Users\benja> ping 8.8.8.8

Envoi d’une requête 'Ping'  8.8.8.8 avec 32 octets de données :
Réponse de 8.8.8.8 : octets=32 temps=58 ms TTL=112
Réponse de 8.8.8.8 : octets=32 temps=46 ms TTL=112
Réponse de 8.8.8.8 : octets=32 temps=44 ms TTL=112
Réponse de 8.8.8.8 : octets=32 temps=40 ms TTL=112

Statistiques Ping pour 8.8.8.8:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 40ms, Maximum = 58ms, Moyenne = 47ms
```

### 2. ARP

☀️ Affichez votre table ARP !

```powershell
PS C:\Users\benja> arp -a

Interface : 192.168.56.1 --- 0xa
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.242.6.7           01-00-5e-72-06-07     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  239.255.255.253       01-00-5e-7f-ff-fd     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 192.168.34.235 --- 0x13
  Adresse Internet      Adresse physique      Type
  192.168.34.20         2c-3b-70-6b-d7-f1     dynamique
  192.168.34.100        80-30-49-40-9b-8b     dynamique
  192.168.34.128        2e-46-d8-19-b7-04     dynamique
  192.168.34.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

☀️ Capture arp2.pcap

```
1	0.000000	AzureWaveTec_37:40:d5	Broadcast	ARP	42	Who has 192.168.34.20? Tell 192.168.34.235

2	0.170069	AzureWaveTec_6b:d7:f1	AzureWaveTec_37:40:d5	ARP	42	192.168.34.20 is at 2c:3b:70:6b:d7:f1

3	5.677238	AzureWaveTec_37:40:d5	Broadcast	ARP	42	Who has 192.168.34.100? Tell 192.168.34.235

4	5.905850	LiteonTechno_40:9b:8b	AzureWaveTec_37:40:d5	ARP	42	192.168.34.100 is at 80:30:49:40:9b:8b
```

### 3.Bonus

Je n'ai pas pu le faire 