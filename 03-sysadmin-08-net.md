# Домашнее задание к занятию "3.8. Компьютерные сети, лекция 3"

#### 1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP
```bash
telnet route-views.routeviews.org
Username: rviews
show ip route x.x.x.x/32
show bgp x.x.x.x/32
```

**ОТВЕТ:**

```bash
# узнаем публичный ip адрес
asamarskii@asm-ubnt:~$ curl 2ip.ru
217.67.179.108

# находим маршрут
asamarskii@asm-ubnt:~$ telnet route-views.routeviews.org
Trying 128.223.51.103...
Connected to route-views.routeviews.org.
Escape character is '^]'
Username: rviews

route-views>show ip route 217.67.179.108
Routing entry for 217.67.176.0/20, supernet
  Known via "bgp 6447", distance 20, metric 0
  Tag 6939, type external
  Last update from 64.71.137.241 7w0d ago
  Routing Descriptor Blocks:
  * 64.71.137.241, from 64.71.137.241, 7w0d ago
      Route metric is 0, traffic share count is 1
      AS Hops 2
      Route tag 6939
      MPLS label: none

route-views>show bgp 217.67.179.108
BGP routing table entry for 217.67.176.0/20, version 904445
Paths: (23 available, best 22, table default)
```

#### 2. Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.

```bash
# создаем конфиги для dummy
asamarskii@asm-ubnt:~$ sudo vim /etc/systemd/network/dummy0.netdev
```

>[NetDev]  
Name=dummy0  
Kind=dummy

```bash
asamarskii@asm-ubnt:~$ sudo vim /etc/systemd/network/dummy0.network
```

>[Match]  
>Name=dummy0
>
>[Network]  
>Address=172.16.16.16/32

```bash
# перезагружаем сетевую подсистему
asamarskii@asm-ubnt:~$ sudo systemctl restart systemd-networkd

# проверяем наличие dummy
asamarskii@asm-ubnt:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: ens18: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 3e:b3:dc:c9:2f:bd brd ff:ff:ff:ff:ff:ff
    inet 10.10.10.226/24 brd 10.10.10.255 scope global ens18
       valid_lft forever preferred_lft forever
    inet6 fe80::3cb3:dcff:fec9:2fbd/64 scope link
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:0f:9f:73:25 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
4: dummy0: <BROADCAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc noqueue state UNKNOWN group default qlen 1000
    link/ether 02:81:c0:3b:54:a1 brd ff:ff:ff:ff:ff:ff
    inet 172.16.16.16/32 scope global dummy0
       valid_lft forever preferred_lft forever
    inet6 fe80::81:c0ff:fe3b:54a1/64 scope link
       valid_lft forever preferred_lft forever

# редактируем конфиг для добавления маршрутов
asamarskii@asm-ubnt:/etc/netplan$ sudo vim 00-installer-config.yaml

network:
  ethernets:
    ens18:
      addresses:
      - 10.10.10.226/24
      gateway4: 10.10.10.1
      routes:
      - to: 192.168.0.0/24
        via: 10.10.10.1
      nameservers:
        addresses:
        - 10.10.10.100
        search:
        - sj.lan
  version: 2

# проверяем наличие маршрута
asamarskii@asm-ubnt:~$ ip ro
default via 10.10.10.1 dev ens18 proto static
10.10.10.0/24 dev ens18 proto kernel scope link src 10.10.10.226
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
192.168.0.0/24 via 10.10.10.1 dev ens18 proto static
```

#### 3. Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров.

```bash
asamarskii@asm-ubnt:~$ ss -lt
State            Recv-Q           Send-Q                     Local Address:Port                       Peer Address:Port           Process
LISTEN           0                4096                       127.0.0.53%lo:domain                          0.0.0.0:*
LISTEN           0                128                              0.0.0.0:ssh                             0.0.0.0:*
LISTEN           0                128                            127.0.0.1:6010                            0.0.0.0:*
LISTEN           0                128                                 [::]:ssh                                [::]:*
LISTEN           0                128                                [::1]:6010                               [::]:*
```

ДЗ производится на чистой машине поэтому на портах только локальный DNS, X11 и SSH

#### 4. Проверьте используемые UDP сокеты в Ubuntu, какие протоколы и приложения используют эти порты?

```bash
asamarskii@asm-ubnt:~$ ss -ul
State            Recv-Q           Send-Q                     Local Address:Port                       Peer Address:Port           Process
UNCONN           0                0                          127.0.0.53%lo:domain                          0.0.0.0:*
```

Только локальный DNS

#### 5. Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали.

![](https://github.com/e2sly4rz/devops-netology/blob/main/images/08net.png)
