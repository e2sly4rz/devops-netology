# Курсовая работа по итогам модуля "DevOps и системное администрирование"

## Процесс установки и настройки ufw

На Ubuntu ufw уже установлен, но не запущен

```bash
# Открываем SSH
asm@netology:~$ sudo ufw allow ssh
Rules updated
Rules updated (v6)

# Открываем HHTPS
asm@netology:~$ sudo ufw allow https
Rules updated
Rules updated (v6)

# Разрешаем любой трафик на lo
asm@netology:~$ sudo ufw allow in on lo
Rule added
Rule added (v6)

# Запускаем работу ufw
asm@netology:~$ sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup

# Проверяем текущие настройки
asm@netology:~$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere
443/tcp                    ALLOW       Anywhere
Anywhere on lo             ALLOW       Anywhere
22/tcp (v6)                ALLOW       Anywhere (v6)
443/tcp (v6)               ALLOW       Anywhere (v6)
Anywhere (v6) on lo        ALLOW       Anywhere (v6)
```

## Процесс установки и выпуска сертификата с помощью hashicorp vault

```bash
asm@netology:~$ vault server -dev -dev-root-token-id root
asm@netology:~$ export VAULT_ADDR=http://127.0.0.1:8200
asm@netology:~$ export VAULT_TOKEN=root
asm@netology:~$ vault secrets enable pki
Success! Enabled the pki secrets engine at: pki/
asm@netology:~$ vault secrets tune -max-lease-ttl=87600h pki
Success! Tuned the secrets engine at: pki/
asm@netology:~$ vault write -field=certificate pki/root/generate/internal common_name="sj.lan" ttl=87600h > CA_cert.crt
asm@netology:~$ vault write pki/config/urls issuing_certificates="$VAULT_ADDR/v1/pki/ca" crl_distribution_points="$VAULT_ADDR/v1/pki/crl"
Success! Data written to: pki/config/urls
asm@netology:~$ vault secrets enable -path=pki_int pki
Success! Enabled the pki secrets engine at: pki_int/
asm@netology:~$ vault secrets tune -max-lease-ttl=43800h pki_int
Success! Tuned the secrets engine at: pki_int/
asm@netology:~$ vault write -format=json pki_int/intermediate/generate/internal common_name="sj.lan Intermediate Authority" | jq -r '.data.csr' > pki_intermediate.csr
asm@netology:~$ vault write -format=json pki/root/sign-intermediate csr=@pki_intermediate.csr format=pem_bundle ttl="43800h" | jq -r '.data.certificate' > intermediate.cert.pem
asm@netology:~$ vault write pki_int/intermediate/set-signed certificate=@intermediate.cert.pem
Success! Data written to: pki_int/intermediate/set-signed
asm@netology:~$ vault write pki_int/roles/sj-dot-lan allowed_domains="sj.lan" allow_subdomains=true max_ttl="750h"
Success! Data written to: pki_int/roles/sj-dot-lan
asm@netology:~$ vault write pki_int/issue/sj-dot-lan common_name="test.sj.lan" ttl="24h"
```

## Процесс установки и настройки сервера nginx

```bash
# Устанавливаем Nginx
asm@netology:~$ sudo apt install nginx

# Корректируем стандартную конфигурацию сайта
asm@netology:~$ sudo vim /etc/nginx/sites-available/default
```

```
server {
        listen 443 ssl default_server;
        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;
        server_name test.ntlg.dev;
        ssl_certificate /etc/nginx/cert.crt;
        ssl_certificate_key /etc/nginx/key.key;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

```bash
# Заносим данные сертификата и ключа по указанному пути
asm@netology:~$ sudo vim /etc/nginx/cert.crt
asm@netology:~$ sudo vim /etc/nginx/key.key

# Загружаем новый конфиг
asm@netology:~$ sudo nginx -s reload
```

## Страница сервера nginx в браузере хоста не содержит предупреждений

![](https://github.com/e2sly4rz/devops-netology/blob/main/images/kurs.jpg)

## Скрипт генерации нового сертификата работает (сертификат сервера ngnix должен быть "зеленым")

```bash
#!/bin/bash

cert_json=/home/asm/cert.json

export VAULT_ADDR=http://127.0.0.1:8200
export VAULT_TOKEN=root

# Generating new certificate
vault write -format=json pki_int/issue/sj-dot-lan common_name="test.sj.lan" ttl="72h" > $cert_json

# Separating json
cat $cert_json | jq -r .data.certificate > /etc/nginx/cert.crt
cat $cert_json | jq -r .data.private_key > /etc/nginx/key.key

# Reload config nginx
systemctl restart nginx

rm $cert_json
```

## Crontab работает (выберите число и время так, чтобы показать что crontab запускается и делает что надо)

```bash
asm@netology:~$ tail -f /var/log/syslog
May 18 11:55:01 netology CRON[4509]: (root) CMD (/home/asm/vault.sh)
May 18 11:55:01 netology systemd[1]: Stopping A high performance web server and a reverse proxy server...
May 18 11:55:01 netology systemd[1]: nginx.service: Succeeded.
May 18 11:55:01 netology systemd[1]: Stopped A high performance web server and a reverse proxy server.
May 18 11:55:01 netology systemd[1]: Starting A high performance web server and a reverse proxy server...
May 18 11:55:01 netology systemd[1]: Started A high performance web server and a reverse proxy server.
May 18 11:55:27 netology kernel: [14887.391196] [UFW BLOCK] IN=ens18 OUT= MAC=01:00:5e:00:00:01:00:0e:1e:88:92:b2:08:00 SRC=0.0.0.0 DST=224.0.0.1 LEN=32 TOS=0x00 PREC=0xC0 TTL=1 ID=0 DF PROTO=2
May 18 11:57:32 netology kernel: [15012.391768] [UFW BLOCK] IN=ens18 OUT= MAC=01:00:5e:00:00:01:00:0e:1e:88:92:b2:08:00 SRC=0.0.0.0 DST=224.0.0.1 LEN=32 TOS=0x00 PREC=0xC0 TTL=1 ID=0 DF PROTO=2
May 18 11:59:37 netology kernel: [15137.392294] [UFW BLOCK] IN=ens18 OUT= MAC=01:00:5e:00:00:01:00:0e:1e:88:92:b2:08:00 SRC=0.0.0.0 DST=224.0.0.1 LEN=32 TOS=0x00 PREC=0xC0 TTL=1 ID=0 DF PROTO=2
May 18 12:00:01 netology CRON[4562]: (root) CMD (/home/asm/vault.sh)
May 18 12:00:02 netology systemd[1]: Stopping A high performance web server and a reverse proxy server...
May 18 12:00:02 netology systemd[1]: nginx.service: Succeeded.
May 18 12:00:02 netology systemd[1]: Stopped A high performance web server and a reverse proxy server.
May 18 12:00:02 netology systemd[1]: Starting A high performance web server and a reverse proxy server...
May 18 12:00:02 netology systemd[1]: Started A high performance web server and a reverse proxy server.
```
