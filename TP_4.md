# TP Réseau 4
## I. DHCP
### 1. Les mains dans le capot

☀️ Capturez un échange DHCP complet

```
1	0.000000	0.0.0.0	255.255.255.255	DHCP	342	DHCP Discover - Transaction ID 0xa368d042

2	0.023201	192.168.34.128	192.168.34.235	DHCP	352	DHCP Offer    - Transaction ID 0xa368d042

3	0.024414	0.0.0.0	255.255.255.255	DHCP	356	DHCP Request  - Transaction ID 0xa368d042

4	0.039469	192.168.34.128	192.168.34.235	DHCP	352	DHCP ACK      - Transaction ID 0xa368d042
```

☀️ Directement dans Wireshark, vous pouvez voir toutes les infos que vous donne  le serveur DHCP

Adresse IP libre dans le réseau : ```Your (client) IP address: 192.168.34.235)```

Serveur DNS indiqué : ```Option: (54) DHCP Server Identifier (192.168.34.128)```

Parcelle de réseau : ```Option: (3) Router : 192.168.34.128```