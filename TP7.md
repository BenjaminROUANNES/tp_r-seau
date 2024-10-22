# TP Réseaux 7

## II. Serveur Web

### 1. HTTP

#### B. Configuration

🌞 Lister les ports en écoute sur la machine

```powershell
[benjam1@web ~]$ sudo ss -lnpt
State  Recv-Q Send-Q  Local Address:Port   Peer Address:Port Process
LISTEN 0      128           0.0.0.0:22          0.0.0.0:*     users:(("sshd",pid=682,fd=3))
LISTEN 0      511           0.0.0.0:80          0.0.0.0:*     users:(("nginx",pid=11476,fd=6),("nginx",pid=11475,fd=6))
LISTEN 0      128              [::]:22             [::]:*     users:(("sshd",pid=682,fd=4))
LISTEN 0      511              [::]:80             [::]:*     users:(("nginx",pid=11476,fd=7),("nginx",pid=11475,fd=7))
[benjam1@web ~]$ sudo ss -lnpt | grep nginx
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=11476,fd=6),("nginx",pid=11475,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=11476,fd=7),("nginx",pid=11475,fd=7))
```

🌞 Ouvrir le port dans le firewall de la machine

```powershell
[benjam1@web ~]$ sudo firewall-cmd --permanent --add-port=80/tcp
success
[benjam1@web ~]$ sudo firewall-cmd --reload
success
[benjam1@web ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 80/tcp
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

#### C. Tests client

🌞 Vérifier que ça a pris effet
```powershell
ben@client1:~$ ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=3.35 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=1.38 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=2.29 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=4 ttl=64 time=1.18 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 1.183/2.048/3.345/0.857 ms
```

```powershell
ben@client1:~$ curl http://sitedefou.tp7.b1
meow !
```

#### D. Analyze

🌞 Capture tcp_http.pcap
```powershell
1	0.000000	10.33.78.240	23.40.113.49	TCP	66	12580 → 80 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 WS=256 SACK_PERM
2	0.011270	23.40.113.49	10.33.78.240	TCP	66	80 → 12580 [SYN, ACK] Seq=0 Ack=1 Win=64240 Len=0 MSS=1460 SACK_PERM WS=128
3	0.011364	10.33.78.240	23.40.113.49	TCP	54	12580 → 80 [ACK] Seq=1 Ack=1 Win=65536 Len=0
4	0.011613	10.33.78.240	23.40.113.49	HTTP	281	GET / HTTP/1.1 
5	0.023418	23.40.113.49	10.33.78.240	TCP	56	80 → 12580 [ACK] Seq=1 Ack=228 Win=64128 Len=0
6	0.023418	23.40.113.49	10.33.78.240	HTTP	317	HTTP/1.1 304 Not Modified 
```

### 2. On rajoute un S

#### A. Config

🌞 Lister les ports en écoute sur la machine

```powershell
[benjam1@web ~]$ sudo ss -lnpt
State      Recv-Q     Send-Q         Local Address:Port         Peer Address:Port    Process
LISTEN     0          511                10.7.1.11:443               0.0.0.0:*        users:(("nginx",pid=11550,fd=6),("nginx",pid=11549,fd=6))
LISTEN     0          128                  0.0.0.0:22                0.0.0.0:*        users:(("sshd",pid=682,fd=3))
LISTEN     0          511                  0.0.0.0:80                0.0.0.0:*        users:(("nginx",pid=11550,fd=7),("nginx",pid=11549,fd=7))
LISTEN     0          128                     [::]:22                   [::]:*        users:(("sshd",pid=682,fd=4))
LISTEN     0          511                     [::]:80                   [::]:*        users:(("nginx",pid=11550,fd=8),("nginx",pid=11549,fd=8))
[benjam1@web ~]$ sudo ss -lnpt | grep nginx
LISTEN 0      511        10.7.1.11:443       0.0.0.0:*    users:(("nginx",pid=11550,fd=6),("nginx",pid=11549,fd=6))
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=11550,fd=7),("nginx",pid=11549,fd=7))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=11550,fd=8),("nginx",pid=11549,fd=8))
```

🌞 Gérer le firewall

```powershell
[benjam1@web ~]$ sudo firewall-cmd --permanent --add-port=443/tcp
success
[benjam1@web ~]$ sudo firewall-cmd --permanent --remove-port=80/tcp
success
[benjam1@web ~]$ sudo firewall-cmd --reload
success
[benjam1@web ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 443/tcp
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

🌞 Capture tcp_https.pcap

```powershell
1	0.000000	10.33.78.240	162.159.133.234	TCP	54	12270 → 443 [ACK] Seq=1 Ack=1 Win=514 Len=0
2	54.570062	10.33.78.240	152.199.19.160	TCP	66	12630 → 443 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 WS=256 SACK_PERM
3	54.607582	152.199.19.160	10.33.78.240	TCP	66	443 → 12630 [SYN, ACK] Seq=0 Ack=1 Win=65535 Len=0 MSS=1460 SACK_PERM WS=512
4	54.607692	10.33.78.240	152.199.19.160	TCP	54	12630 → 443 [ACK] Seq=1 Ack=1 Win=65536 Len=0
5	54.608710	10.33.78.240	152.199.19.160	TCP	1514	12630 → 443 [ACK] Seq=1 Ack=1 Win=65536 Len=1460 [TCP PDU reassembled in 6]
6	54.608710	10.33.78.240	152.199.19.160	TLSv1.3	661	Client Hello (SNI=az764295.vo.msecnd.net)
7	54.626103	152.199.19.160	10.33.78.240	TLSv1.3	153	Hello Retry Request, Change Cipher Spec
8	54.626682	10.33.78.240	152.199.19.160	TLSv1.3	935	Change Cipher Spec, Client Hello (SNI=az764295.vo.msecnd.net)
9	54.643566	152.199.19.160	10.33.78.240	TLSv1.3	1514	Server Hello, Application Data
10	54.643566	152.199.19.160	10.33.78.240	TCP	1514	443 → 12630 [ACK] Seq=1560 Ack=2949 Win=72704 Len=1460
11	54.643566	152.199.19.160	10.33.78.240	TCP	1230	443 → 12630 [PSH, ACK] Seq=3020 Ack=2949 Win=72704 Len=1176
12	54.643640	10.33.78.240	152.199.19.160	TCP	54	12630 → 443 [ACK] Seq=2949 Ack=4196 Win=65536 Len=0
```

