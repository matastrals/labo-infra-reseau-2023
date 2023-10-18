## TP Niveau 1

Quels sont les deux différents types d'hyperviseur existant, et quelles sont leur différence ?

Il y a deux types d'hyperviseurs : hyperviseurs de type 1 et 2.
L'hyperviseur de type 1, nommé « bare metal » s’exécute directement sur le matériel de l’hôte. L'hyperviseur de type 2, nommé « hébergé » s’exécute sous forme d’une couche logicielle sur un système d’exploitation, comme n’importe quel autre programme informatique. 

[Ip 1re vm](./Ip_landing_vm1.png)

[Ip 2nd vm](./Ip_landing_vm2.png)

##### Changez le nom d'hôte des machines pour avoir respectivement vm-landing1 et vm-landing2

```
[matastral@localhost ~]$ sudo nano /etc/hostname
[matastral@vm-landing1 ~]$
```

```
[matastral@localhost ~]$ sudo nano /etc/hostname
[matastral@vm-landing2 ~]$
```

##### Trouvez l'adresse IP locale des machines

```
[matastral@vm-landing1 ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1c:94:e0 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86172sec preferred_lft 86172sec
    inet6 fe80::a00:27ff:fe1c:94e0/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:f1:5b:02 brd ff:ff:ff:ff:ff:ff
    inet 172.16.64.2/24 brd 172.16.64.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fef1:5b02/64 scope link
       valid_lft forever preferred_lft forever
```

```
[matastral@vm-landing2 ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1c:94:e0 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86256sec preferred_lft 86256sec
    inet6 fe80::a00:27ff:fe1c:94e0/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:bf:70:f7 brd ff:ff:ff:ff:ff:ff
    inet 172.16.64.3/24 brd 172.16.64.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:febf:70f7/64 scope link
       valid_lft forever preferred_lft forever
```

##### Quelle est l'adresse de broadcast ?

L'adresse de broadcast est 172.16.64.255

##### Trouvez le masque de sous-réseau des machines

```
[matastral@vm-landing1 ~]$ ip a show enp0s8
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:f1:5b:02 brd ff:ff:ff:ff:ff:ff
    inet 172.16.64.2/24 brd 172.16.64.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fef1:5b02/64 scope link
       valid_lft forever preferred_lft forever
```

```
[matastral@vm-landing2 ~]$ ip a show enp0s8
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:bf:70:f7 brd ff:ff:ff:ff:ff:ff
    inet 172.16.64.3/24 brd 172.16.64.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:febf:70f7/64 scope link
       valid_lft forever preferred_lft forever
```

Le masque est donc le /24 qui est 255.255.255.0

##### Trouvez l'adresse MAC des machines

```
[matastral@vm-landing1 ~]$ ip link show enp0s8
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:f1:5b:02 brd ff:ff:ff:ff:ff:ff
```

```
[matastral@vm-landing2 ~]$ ip link show enp0s8
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:bf:70:f7 brd ff:ff:ff:ff:ff:ff
```

##### Pingez l'adresse publique du site www.ynov.com avec une des deux machines

```
[matastral@vm-landing1 ~]$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
^C64 bytes from 172.67.74.226: icmp_seq=1 ttl=56 time=16.3 ms

--- ynov.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 16.309/16.309/16.309/0.000 ms
```

##### Essayez de lire le contenu du fichier /var/log/lastlog.   

```
[labo-user1@vm-landing1 ~]$ cat /var/log/tallylog
cat: /var/log/tallylog: Permission denied
```

##### Que se passe-t-il ? Pourquoi ?

On peut pas le lire par manque de droit.

##### Il y aura toujours une erreur. Après avoir recherche sur Google la significance du groupe wheel dans Linux, pourquoi cette erreur est-elle toujours présente ?

Parcequ'avoir les droits root ne suffisent pas. Il faut inclure sudo pour pouvoir les utilisez.

##### Il n'y aura plus d'erreur. Pourquoi ?

Parcequ'on précise qu'on utilise les droits avec "sudo".

##### Ca devrait marcher. Pourquoi ?

Car root est l'utilisateur suprème, il possède tout les droits.

##### Pingez vm-landing2 avec vm-landing1

```
[root@vm-landing1 matastral]# ping 172.16.64.3
PING 172.16.64.3 (172.16.64.3) 56(84) bytes of data.
64 bytes from 172.16.64.3: icmp_seq=1 ttl=64 time=0.375 ms
64 bytes from 172.16.64.3: icmp_seq=2 ttl=64 time=0.427 ms
^C
--- 172.16.64.3 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1043ms
rtt min/avg/max/mdev = 0.375/0.401/0.427/0.026 ms
```

##### Vérifiez leur version

🚂🚃​🚃​🚃​​TCHOU TCHOU
```
[root@vm-landing1 matastral]# dnsmasq --version
Dnsmasq version 2.85  Copyright (c) 2000-2021 Simon Kelley
[root@vm-landing1 matastral]# htop --version
htop 3.2.2
```

##### pingez google.com

```
[root@vm-landing1 matastral]# ping google.com
PING google.com (216.58.214.174) 56(84) bytes of data.
^C64 bytes from 216.58.214.174: icmp_seq=1 ttl=115 time=26.1 ms

--- google.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 26.145/26.145/26.145/0.000 ms
```

##### Vérifiez leur version

```
[matastral@vm-landing2 ~]$ htop --version
htop 3.2.2
[matastral@vm-landing2 ~]$ fail2ban-client --version
Fail2Ban v1.0.2
[matastral@vm-landing2 ~]$ unzip -v
UnZip 6.00 of 20 April 2009, by Info-ZIP.  Maintained by C. Spieler.  Send
```

##### pingez cloudflare.com

```
[matastral@vm-landing2 ~]$ ping cloudfare.com
PING cloudfare.com (188.114.96.7) 56(84) bytes of data.
^C64 bytes from 188.114.96.7: icmp_seq=1 ttl=56 time=31.6 ms

--- cloudfare.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 31.552/31.552/31.552/0.000 ms
```

##### Quelle est l'utilité de ce type de carte réseau ?

L'utilité des cartes réseau Host Only permet à l'utilisateur de communiquer à sa vm depuuis son pc et cela permet aussi de faire communiquer les vm entre elles.