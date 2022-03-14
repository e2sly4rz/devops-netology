# Домашнее задание к занятию "3.6. Компьютерные сети, лекция 1"

#### 1. Работа c HTTP через телнет.
- Подключитесь утилитой телнет к сайту stackoverflow.com
`telnet stackoverflow.com 80`
- отправьте HTTP запрос
```bash
GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter]
```
- В ответе укажите полученный HTTP код, что он означает?

```bash
e2sly4rz@DESKTOP-43OOABH:~$ telnet stackoverflow.com 80
Trying 151.101.129.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com
```
```bash
# Код ответа 301 говорит о том, что запрашиваемый ресурс был перемещен
HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate

# Здесь мы видим куда был перемещен запрашиваемый ресурс
location: https://stackoverflow.com/questions
x-request-guid: 653d0c4b-b09f-414a-a048-10fccdd22dd4
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Mon, 14 Mar 2022 10:04:53 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-fra19142-FRA
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1647252293.089483,VS0,VE93
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=5c45de77-7252-272a-9d2b-878c9e8e493c; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```

#### 2. Повторите задание 1 в браузере, используя консоль разработчика F12.
- откройте вкладку `Network`
- отправьте запрос http://stackoverflow.com
- найдите первый ответ HTTP сервера, откройте вкладку `Headers`
- укажите в ответе полученный HTTP код.
- **307**
- проверьте время загрузки страницы, какой запрос обрабатывался дольше всего?
- **страница загрузилась за 1.13сек. Дольше всего обрабатывался запрос получения страницы**
- приложите скриншот консоли браузера в ответ.

![](https://github.com/e2sly4rz/devops-netology/blob/main/images/06net.png)

#### 3. Какой IP адрес у вас в интернете?

```bash
e2sly4rz@DESKTOP-43OOABH:~$ curl ifconfig.me
109.173.124.140
```

#### 4. Какому провайдеру принадлежит ваш IP адрес? Какой автономной системе AS? Воспользуйтесь утилитой `whois`

```bash
e2sly4rz@DESKTOP-43OOABH:~$ whois 109.173.124.140
% This is the RIPE Database query service.
% The objects are in RPSL format.
%
% The RIPE Database is subject to Terms and Conditions.
% See http://www.ripe.net/db/support/db-terms-conditions.pdf

% Note: this output has been filtered.
%       To receive output for a database update, use the "-B" flag.

% Information related to '109.173.64.0 - 109.173.127.255'

% Abuse contact for '109.173.64.0 - 109.173.127.255' is 'abuse@rt.ru'

inetnum:        109.173.64.0 - 109.173.127.255
# Наименования организации которой принадлежит адрес
netname:        NCN-BBCUST                        
descr:          NCNET Broadband customers
country:        RU
admin-c:        NCN7-RIPE
tech-c:         NCN7-RIPE
status:         ASSIGNED PA
mnt-by:         NCNET-MNT
mnt-lower:      NCNET-MNT
mnt-routes:     NCNET-MNT
created:        2010-03-12T13:52:11Z
last-modified:  2010-03-12T13:52:11Z
source:         RIPE

role:           NCNET NCC Operations
address:        National Cable Networks
address:        Nagatinskaya str., 1, bldn. 26
address:        117105 Moscow, Russia
org:            ORG-NCN1-RIPE
admin-c:        RVP-RIPE
tech-c:         RVP-RIPE
phone:          +7 495 6859542
fax-no:         +7 495 6859530
mnt-by:         NCNET-MNT
nic-hdl:        NCN7-RIPE
created:        2007-03-26T07:46:58Z
last-modified:  2015-10-12T11:53:05Z
source:         RIPE # Filtered
abuse-mailbox:  abuse@moscow.rt.ru

% Information related to '109.173.64.0/18AS42610'

route:          109.173.64.0/18
descr:          NCNET
# Указание на номер автономной системы
origin:         AS42610
mnt-by:         NCNET-MNT
mnt-lower:      NCNET-MNT
created:        2009-12-30T09:49:28Z
last-modified:  2009-12-30T09:49:28Z
source:         RIPE

% This query was served by the RIPE Database Query Service version 1.102.2 (BLAARKOP)
```

#### 5. Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой `traceroute`

```bash
e2sly4rz@DESKTOP-43OOABH:~$ traceroute -A 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  DESKTOP-43OOABH.mshome.net (172.25.0.1) [*]  1.243 ms  0.972 ms  0.890 ms
 2  router.lan (192.168.4.1) [*]  26.793 ms  26.737 ms  26.702 ms
 3  broadband-90-154-77-227.ip.moscow.rt.ru (90.154.77.227) [AS42610]  26.124 ms  53.242 ms  53.214 ms
 4  77.37.250.200 (77.37.250.200) [AS42610]  53.197 ms  53.037 ms  52.932 ms
 5  77.37.250.249 (77.37.250.249) [AS42610]  52.944 ms  52.925 ms  52.909 ms
 6  72.14.209.81 (72.14.209.81) [AS15169]  52.770 ms  24.927 ms  24.878 ms
 7  * * *
 8  108.170.227.74 (108.170.227.74) [AS15169]  7.405 ms  7.055 ms 108.170.226.176 (108.170.226.176) [AS15169]  7.840 ms
 9  * 108.170.250.130 (108.170.250.130) [AS15169]  8.906 ms 108.170.250.99 (108.170.250.99) [AS15169]  8.841 ms
10  * * 209.85.255.136 (209.85.255.136) [AS15169]  89.579 ms
11  209.85.254.20 (209.85.254.20) [AS15169]  89.668 ms 72.14.238.168 (72.14.238.168) [AS15169]  89.500 ms 172.253.65.82 (172.253.65.82) [AS15169]  89.188 ms
12  142.250.238.179 (142.250.238.179) [AS15169]  89.272 ms * 172.253.51.247 (172.253.51.247) [AS15169]  82.860 ms
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  dns.google (8.8.8.8) [AS15169]  17.590 ms  21.223 ms *
```

#### 6. Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка - delay?

```bash
e2sly4rz@DESKTOP-43OOABH:~$ mtr -z -c 100 -r 8.8.8.8
Start: 2022-03-14T14:21:49+0300
HOST: DESKTOP-43OOABH             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1. AS???    DESKTOP-43OOABH.msh  0.0%   100    1.2   1.1   0.3   1.4   0.2
  2. AS???    router.lan           0.0%   100    3.0   3.1   1.6   8.5   1.0
  3. AS12389  broadband-90-154-77  0.0%   100    4.3   5.6   3.1 107.5  10.5
  4. AS42610  77.37.250.200       34.0%   100    5.4   4.6   3.4  14.5   1.4
  5. AS42610  77.37.250.249        1.0%   100    5.8  10.3   4.1 209.5  26.2
  6. AS15169  72.14.209.81         0.0%   100    5.5   7.7   5.1  59.9   6.8
  7. AS15169  209.85.250.231       0.0%   100    5.3   6.3   5.0  16.6   1.3
  8. AS15169  108.170.250.99       0.0%   100    6.0   6.5   4.7  14.6   1.2
  9. AS15169  142.251.49.24       75.0%   100   21.8  23.2  21.1  50.1   5.6
  # Участок с бОльшей средней задержкой
 10. AS15169  72.14.238.168        0.0%   100   21.1  25.0  20.1  89.2  10.2
 11. AS15169  216.239.63.129       0.0%   100   18.9  19.7  17.8  90.9   7.2
 12. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 13. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 14. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 15. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 16. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 17. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 18. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 19. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 20. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 21. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 22. AS???    ???                 100.0   100    0.0   0.0   0.0   0.0   0.0
 23. AS15169  dns.google           0.0%   100   20.4  22.2  19.7  60.7   4.9
 ```

#### 7. Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой `dig`

```bash
e2sly4rz@DESKTOP-43OOABH:~$ dig +trace dns.google | grep dns.google
dns.google.             10800   IN      NS      ns4.zdns.google.
dns.google.             10800   IN      NS      ns2.zdns.google.
dns.google.             10800   IN      NS      ns3.zdns.google.
dns.google.             10800   IN      NS      ns1.zdns.google.
```

```bash
e2sly4rz@DESKTOP-43OOABH:~$ dig dns.google | grep dns.google
;dns.google.                    IN      A
dns.google.             0       IN      A       8.8.4.4
dns.google.             0       IN      A       8.8.8.8
```

#### 8. Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой `dig`

```bash
e2sly4rz@DESKTOP-43OOABH:~$ dig -x 8.8.8.8
;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.          IN      PTR

e2sly4rz@DESKTOP-43OOABH:~$ dig -x 8.8.4.4
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR
```
