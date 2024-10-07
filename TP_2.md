# TP Réseau 2

## I. Simplest LAN

### 1. Quelques pings

🌞 Prouvez que votre configuration est effective

```
ben@ben-ubuntu:~$ ip addr show enp0s8
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:31:89:12 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.104/24 brd 192.168.56.255 scope global dynamic noprefixroute enp0s8
       valid_lft 463sec preferred_lft 463sec
    inet6 fe80::9416:24ef:a93f:cfee/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

🌞 Tester que votre LAN + votre adressage IP est fonctionnel

``` powershell
PS C:\Users\benja> ping 192.168.56.104

Envoi d’une requête 'Ping'  192.168.56.104 avec 32 octets de données :
Réponse de 192.168.56.104 : octets=32 temps<1ms TTL=64
Réponse de 192.168.56.104 : octets=32 temps=1 ms TTL=64
Réponse de 192.168.56.104 : octets=32 temps=1 ms TTL=64
Réponse de 192.168.56.104 : octets=32 temps=1 ms TTL=64

Statistiques Ping pour 192.168.56.104:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 1ms, Moyenne = 0ms
```

```
ben@ben-ubuntu:~$ ping 192.168.56.1
PING 192.168.56.1 (192.168.56.1) 56(84) bytes of data.
^C
--- 192.168.56.1 ping statistics ---
9 packets transmitted, 0 received, 100% packet loss, time 8202ms
```


🌞 Capture de ping

```
5	26.485571	192.168.56.1	192.168.56.104	SSH	90	Client: Encrypted packet (len=36)

6	26.487527	192.168.56.104	192.168.56.1	SSH	90	Server: Encrypted packet (len=36)

7	26.527445	192.168.56.1	192.168.56.104	TCP	54	55592 → 22 [ACK] Seq=37 Ack=37 Win=8193 Len=0

8	26.655628	192.168.56.1	192.168.56.104	SSH	90	Client: Encrypted packet (len=36)

9	26.657097	192.168.56.104	192.168.56.1	SSH	90	Server: Encrypted packet (len=36)

10	26.696679	192.168.56.1	192.168.56.104	TCP	54	55592 → 22 [ACK] Seq=73 Ack=73 Win=8193 Len=0

11	26.904739	192.168.56.1	192.168.56.104	SSH	90	Client: Encrypted packet (len=36)

12	26.906150	192.168.56.104	192.168.56.1	SSH	90	Server: Encrypted packet (len=36)
```

## II. Utilisation des ports

### 1. Animal numérique

🌞 Sur le PC serveur

```
PS C:\Users\benja\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe -l -p 9999
```

🌞 Sur le PC serveur toujours

```powershell
PS C:\WINDOWS\system32> netstat -a -b -n

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING
  RpcSs
 [svchost.exe]
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING
 Impossible d’obtenir les informations de propriétaire
  TCP    0.0.0.0:5040           0.0.0.0:0              LISTENING
  CDPSvc
 [svchost.exe]
  TCP    0.0.0.0:7680           0.0.0.0:0              LISTENING
```

🌞 Sur le PC client

```
ben@ben-ubuntu:~$ nc 192.168.56.1 9999
```

🌞 Echangez-vous des messages

```
ben@ben-ubuntu:~$ nc 192.168.56.1 9999
netstat -a -b -nnetstat -a -b -n
lol
pc
fortnite battle passx
```

```powershell
PS C:\Users\benja\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe -l -p 9999
netstat -a -b -nnetstat -a -b -n
lol
pc
fortnite battle passx
```

🌞 Utilisez une commande qui permet de voir la connexion en cour

```powershell
PS C:\WINDOWS\system32> netstat

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    10.33.78.240:49439     20.199.120.151:https   ESTABLISHED
  TCP    10.33.78.240:54221     20.199.120.85:https    ESTABLISHED
  TCP    10.33.78.240:54452     52.123.200.50:https    ESTABLISHED
  TCP    10.33.78.240:55504     52.123.137.10:https    ESTABLISHED
  TCP    10.33.78.240:55509     45:https               ESTABLISHED
  TCP    10.33.78.240:55524     wi-in-f188:https       ESTABLISHED
```

🌞 Faites une capture Wireshark complète d'un échange

```
6	1.031908	192.168.56.104	192.168.56.1	TCP	74	55242 → 9999 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=1023945807 TSecr=0 WS=128

7	1.032018	192.168.56.1	192.168.56.104	TCP	74	9999 → 55242 [SYN, ACK] Seq=0 Ack=1 Win=65535 Len=0 MSS=1460 WS=256 SACK_PERM TSval=953169728 TSecr=1023945807

8	1.032284	192.168.56.104	192.168.56.1	TCP	66	55242 → 9999 [ACK] Seq=1 Ack=1 Win=64256 Len=0 TSval=1023945807 TSecr=953169728
```

🌞 Inversez les rôles

```
nc -l 9999
```
```powershell
PS C:\Users\benja\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe 192.168.56.104 9999
```

```
50	119.921079	192.168.56.1	192.168.56.104	TCP	66	55961 → 9999 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 WS=256 SACK_PERM

51	119.921450	192.168.56.104	192.168.56.1	TCP	66	9999 → 55961 [SYN, ACK] Seq=0 Ack=1 Win=64240 Len=0 MSS=1460 SACK_PERM WS=128

52	119.921487	192.168.56.1	192.168.56.104	TCP	54	55961 → 9999 [ACK] Seq=1 Ack=1 Win=262656 Len=0
```

## III. Analyse de vos applications usuelles

### 1. Serveur web

```
1314	31.366456	10.33.78.240	185.125.190.48	TCP	66	56237 → 80 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 WS=256 SACK_PERM

1315	31.384558	185.125.190.48	10.33.78.240	TCP	66	80 → 56237 [SYN, ACK] Seq=0 Ack=1 Win=64240 Len=0 MSS=1460 SACK_PERM WS=128

1316	31.384604	10.33.78.240	185.125.190.48	TCP	54	56237 → 80 [ACK] Seq=1 Ack=1 Win=131328 Len=0

1317	31.385588	10.33.78.240	185.125.190.48	HTTP	142	GET / HTTP/1.1 

1318	31.403982	185.125.190.48	10.33.78.240	TCP	56	[TCP Previous segment not captured] 80 → 56237 [FIN, ACK] Seq=190 Ack=89 Win=64256 Len=0

1319	31.403982	185.125.190.48	10.33.78.240	TCP	243	[TCP Out-Of-Order] 80 → 56237 [PSH, ACK] Seq=1 Ack=89 Win=64256 Len=189

1320	31.404018	10.33.78.240	185.125.190.48	TCP	54	[TCP Dup ACK 1316#1] 56237 → 80 [ACK] Seq=89 Ack=1 Win=131328 Len=0
```

### 2. Autres services

Spotify
```
1	0.000000	10.33.78.240	104.199.65.9	TCP	54	56286 → 4070 [FIN, ACK] Seq=1 Ack=1 Win=512 Len=0

2	0.024533	104.199.65.9	10.33.78.240	TCP	56	4070 → 56286 [FIN, ACK] Seq=1 Ack=2 Win=6 Len=0

3	0.024593	10.33.78.240	104.199.65.9	TCP	54	56286 → 4070 [ACK] Seq=2 Ack=2 Win=512 Len=0

4	3.582180	10.33.78.240	104.199.65.9	TCP	66	56474 → 4070 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 WS=256 SACK_PERM
```

Discord
```
1	0.000000	162.159.133.234	10.33.78.240	TLSv1.2	103	Application Data

2	0.053869	10.33.78.240	162.159.133.234	TCP	54	56344 → 443 [ACK] Seq=1 Ack=50 Win=513 Len=0

3	1.442371	162.159.133.234	10.33.78.240	TLSv1.2	109	Application Data

4	1.442371	162.159.133.234	10.33.78.240	TLSv1.2	96	Application Data
```

Opera
```
