# Домашнее задание к занятию "3.9. Элементы безопасности информационных систем"

#### 1. Установите Bitwarden плагин для браузера. Зарегестрируйтесь и сохраните несколько паролей.

![](https://github.com/e2sly4rz/devops-netology/blob/main/images/09sec01.jpg)

#### 2. Установите Google authenticator на мобильный телефон. Настройте вход в Bitwarden акаунт через Google authenticator OTP.

![](https://github.com/e2sly4rz/devops-netology/blob/main/images/09sec02.jpg)

#### 3. Установите apache2, сгенерируйте самоподписанный сертификат, настройте тестовый сайт для работы по HTTPS.

```bash
# устанавливаем apache
asamarskii@asm-ubnt:~$ sudo apt install -y apache2

# подключаем модуль ssl
asamarskii@asm-ubnt:~$ sudo a2enmod ssl
asamarskii@asm-ubnt:~$ sudo a2ensite default-ssl

# генерируем самоподписанный сертификат
asamarskii@asm-ubnt:~$ sudo openssl req -x509 -nodes -newkey rsa:2048 -keyout /etc/ssl/private/apache-ss.key -out /etc/ssl/certs/apache-ss.crt
Generating a RSA private key
..................+++++
..............+++++
writing new private key to '/etc/ssl/private/apache-ss.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:RU
State or Province Name (full name) [Some-State]:Moscow
Locality Name (eg, city) []:Moscow
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Testology Ltd
Organizational Unit Name (eg, section) []:HQ
Common Name (e.g. server FQDN or YOUR name) []:asm-ubnt.sj.lan
Email Address []:e2sly4rz@gmail.com

# добавляем имя и редирект в конфигурацию сайта
asamarskii@asm-ubnt:~$ sudo vim /etc/apache2/sites-available/000-default.conf

ServerName asm-ubnt.sj.lan
Redirect / https://asm-ubnt.sj.lan

# добавляем пути до сертификата в конфигурации ssl
asamarskii@asm-ubnt:~$ sudo vim /etc/apache2/sites-available/default-ssl.conf

SSLCertificateFile      /etc/ssl/certs/apache-ss.crt
SSLCertificateKeyFile /etc/ssl/private/apache-ss.key

# перезапускаем aoache
asamarskii@asm-ubnt:~$ sudo service apache2 restart
```

![](https://github.com/e2sly4rz/devops-netology/blob/main/images/09sec03.jpg)

#### 4. Проверьте на TLS уязвимости произвольный сайт в интернете (кроме сайтов МВД, ФСБ, МинОбр, НацБанк, РосКосмос, РосАтом, РосНАНО и любых госкомпаний, объектов КИИ, ВПК ... и тому подобное).

```bash
asamarskii@asm-ubnt:~/testssl/testssl.sh$ sudo ./testssl.sh https://murmanhunt.ru/

Rating (experimental)

Rating specs (not complete)  SSL Labs 'SSL Server Rating Guide' (version 2009q from 2020-01-30)
Specification documentation  https://github.com/ssllabs/research/wiki/SSL-Server-Rating-Guide
Protocol Support (weighted)  100 (30)
Key Exchange     (weighted)  90 (27)
Cipher Strength  (weighted)  90 (36)
Final Score                  93
Overall Grade                A
Grade cap reasons            Grade capped to A. HSTS is not offered
```

#### 5. Установите на Ubuntu ssh сервер, сгенерируйте новый приватный ключ. Скопируйте свой публичный ключ на другой сервер. Подключитесь к серверу по SSH-ключу.

```powershell
# создаем ssh ключ
PS C:\Users\alexander.samarskii> ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\alexander.samarskii/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in id_rsa.
Your public key has been saved in id_rsa.pub.
The key fingerprint is:
SHA256:qnfQPXdtkO3kojdAkKg0u5F6gyvO/ewdfKPAbBBRT3U sj\asm@KATYA
The key's randomart image is:
+---[RSA 3072]----+
|    ... .o..E    |
|     .oo. o.     |
|    .. =.  .   o |
|     .=     . o o|
|    .o +S. .   * |
|    o+=o. o o o =|
|     o*oo oo + o |
| ....+.o.+ .. o  |
| .o.o++.o    . . |
+----[SHA256]-----+

# передаем ssh ключ на сервер
PS C:\Users\alexander.samarskii> type $env:USERPROFILE\.ssh\id_rsa.pub | ssh asamarskii@10.10.10.226 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
The authenticity of host '10.10.10.226 (10.10.10.226)' can't be established.
ECDSA key fingerprint is SHA256:dZmSSh4Fo/lRdDj1xHM6tXGM6Vd9qln+oceo23J95rQ.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.10.226' (ECDSA) to the list of known hosts.
asamarskii@10.10.10.226's password:

# подключаемся по ssh
PS C:\Users\alexander.samarskii> ssh asamarskii@10.10.10.226
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-105-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Ср 30 мар 2022 11:40:39 UTC

  System load:  0.36               Processes:                132
  Usage of /:   42.9% of 14.94GB   Users logged in:          1
  Memory usage: 7%                 IPv4 address for docker0: 172.17.0.1
  Swap usage:   0%                 IPv4 address for ens18:   10.10.10.226


0 updates can be applied immediately.


Last login: Wed Mar 30 10:36:37 2022 from 10.10.12.3
asamarskii@asm-ubnt:~$
```

#### 6. Переименуйте файлы ключей из задания 5. Настройте файл конфигурации SSH клиента, так чтобы вход на удаленный сервер осуществлялся по имени сервера.

Файл конфигурации ssh

```
Host netology
  HostName asm-ubnt.sj.lan
  User asamarskii
    IdentityFile ~/.ssh/netology
```
Подключаемся

```powershell
PS C:\Users\alexander.samarskii> ssh netology
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-105-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Ср 30 мар 2022 12:27:20 UTC

  System load:  0.08               Processes:                126
  Usage of /:   42.9% of 14.94GB   Users logged in:          1
  Memory usage: 7%                 IPv4 address for docker0: 172.17.0.1
  Swap usage:   0%                 IPv4 address for ens18:   10.10.10.226


0 updates can be applied immediately.


Last login: Wed Mar 30 11:40:39 2022 from 10.10.12.3
asamarskii@asm-ubnt:~$
```

#### 7. Соберите дамп трафика утилитой tcpdump в формате pcap, 100 пакетов. Откройте файл pcap в Wireshark.

```bash
asamarskii@asm-ubnt:~$ sudo tcpdump -c 100 -w dump.pcap
[sudo] password for asamarskii:
tcpdump: listening on ens18, link-type EN10MB (Ethernet), capture size 262144 bytes
100 packets captured
103 packets received by filter
0 packets dropped by kernel
```

![](https://github.com/e2sly4rz/devops-netology/blob/main/images/09sec04.jpg)
