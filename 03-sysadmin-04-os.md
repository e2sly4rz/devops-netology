## Домашнее задание к занятию "3.4. Операционные системы, лекция 2"

#### 1. На лекции мы познакомились с node_exporter. В демонстрации его исполняемый файл запускался в background. Этого достаточно для демо, но не для настоящей production-системы, где процессы должны находиться под внешним управлением. Используя знания из лекции по systemd, создайте самостоятельно простой unit-файл для node_exporter:
- поместите его в автозагрузку,
- предусмотрите возможность добавления опций к запускаемому процессу через внешний файл (посмотрите, например, на `systemctl cat cron`),
- удостоверьтесь, что с помощью systemctl процесс корректно стартует, завершается, а после перезагрузки автоматически поднимается.

```bash
# Ставим и запускаем node_exporter
asamarskii@asm-tst:~$ wget https://github.com/prometheus/node_exporter/releases/download/v1.3.1/node_exporter-1.3.1.linux-amd64.tar.gz
asamarskii@asm-tst:~$ tar xvfz node_exporter-1.3.1.linux-amd64.tar.gz
asamarskii@asm-tst:~$ cd node_exporter-1.3.1.linux-amd64/
asamarskii@asm-tst:~$ ./node_exporter

# Проверяем доступ
asamarskii@asm-tst:~$ curl localhost:9100
<html>
                        <head><title>Node Exporter</title></head>
                        <body>
                        <h1>Node Exporter</h1>
                        <p><a href="/metrics">Metrics</a></p>
                        </body>
                        </html>
```

Создаем unit-файл:

```bash
[Unit]
Description=Node Exporter

[Service]
# Предусматриваем возможность добавления опций к запускаемому процессу через внешний файл
# Сам файл также необходимо создать
EnvironmentFile=/home/asamarskii/node_exporter-1.3.1.linux-amd64/default/node_exporter
ExecStart=/home/asamarskii/node_exporter-1.3.1.linux-amd64/node_exporter

[Install]
WantedBy=multi-user.target
```

Добавляем в автозагрузку:

```bash
asamarskii@asm-tst:~$ sudo systemctl enable node_exporter.service
Created symlink /etc/systemd/system/multi-user.target.wants/node_exporter.service → /etc/systemd/system/node_exporter.service.
```

Тестируем запуск, остановку и автозагрузку

```bash
# После запуска системы проверяем работу автозагрузки
asamarskii@asm-tst:~$ sudo systemctl status node_exporter.service
● node_exporter.service - Node Exporter
     Loaded: loaded (/etc/systemd/system/node_exporter.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2022-02-16 13:19:22 UTC; 59s ago
   Main PID: 653 (node_exporter)
      Tasks: 4 (limit: 2274)
     Memory: 14.3M
     CGroup: /system.slice/node_exporter.service
             └─653 /home/asamarskii/node_exporter-1.3.1.linux-amd64/node_exporter

# Останавливаем процесс
asamarskii@asm-tst:~$ sudo systemctl stop node_exporter.service
asamarskii@asm-tst:~$ sudo systemctl status node_exporter.service
● node_exporter.service - Node Exporter
     Loaded: loaded (/etc/systemd/system/node_exporter.service; enabled; vendor preset: enabled)
     Active: inactive (dead) since Wed 2022-02-16 13:23:14 UTC; 2s ago
    Process: 653 ExecStart=/home/asamarskii/node_exporter-1.3.1.linux-amd64/node_exporter (code=killed, signal=TERM)
   Main PID: 653 (code=killed, signal=TERM)

# Запускаем процесс
asamarskii@asm-tst:~$ sudo systemctl start node_exporter.service
asamarskii@asm-tst:~$ sudo systemctl status node_exporter.service
● node_exporter.service - Node Exporter
     Loaded: loaded (/etc/systemd/system/node_exporter.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2022-02-16 13:24:41 UTC; 2s ago
   Main PID: 2765 (node_exporter)
      Tasks: 4 (limit: 2274)
     Memory: 2.6M
     CGroup: /system.slice/node_exporter.service
             └─2765 /home/asamarskii/node_exporter-1.3.1.linux-amd64/node_exporter
```

#### 2. Ознакомьтесь с опциями node_exporter и выводом `/metrics` по-умолчанию. Приведите несколько опций, которые вы бы выбрали для базового мониторинга хоста по CPU, памяти, диску и сети.

CPU:
- node_cpu_seconds_total{mode="idle"}
- node_cpu_seconds_total{mode='system'}

RAM:
- node_memory_MemAvailable_bytes
- node_memory_MemFree_bytes
- node_memory_MemTotal_bytes
- node_memory_SwapFree_bytes
- node_memory_SwapTotal_bytes

DISK/FS:
- node_disk_io_time_seconds_total
- node_disk_read_bytes_total
- node_disk_written_bytes_total
- node_filesystem_free_bytes

NET:
- node_network_up
- node_network_carrier_down_changes_total
- node_network_receive_bytes_total
- node_network_receive_packets_total
- node_network_receive_errs_total
- node_network_transmit_bytes_total
- node_network_transmit_packets_total
- node_network_transmit_errs_total

#### 3. Установите в свою виртуальную машину Netdata. Воспользуйтесь готовыми пакетами для установки (`sudo apt install -y netdata`). После успешной установки:
- в конфигурационном файле `/etc/netdata/netdata.conf` в секции [web] замените значение с localhost на `bind to = 0.0.0.0`,
- добавьте в Vagrantfile проброс порта Netdata на свой локальный компьютер и сделайте `vagrant reload`:
> config.vm.network "forwarded_port", guest: 19999, host: 19999

#### После успешной перезагрузки в браузере на своем ПК (не в виртуальной машине) вы должны суметь зайти на `localhost:19999`. Ознакомьтесь с метриками, которые по умолчанию собираются Netdata и с комментариями, которые даны к этим метрикам.

![](images/netdata01.jpg?raw=true)
![](images/netdata01.jpg?raw=true)

#### 4. Можно ли по выводу `dmesg` понять, осознает ли ОС, что загружена не на настоящем оборудовании, а на системе виртуализации?

Да.
В моем случае об этом говорит строка:

> [    0.000000] Hypervisor detected: KVM

Дальше systemd также определяет виртуализацию:

> [    4.803868] systemd[1]: Detected virtualization kvm.

#### 5. Как настроен `sysctl fs.nr_open` на системе по-умолчанию? Узнайте, что означает этот параметр. Какой другой существующий лимит не позволит достичь такого числа (`ulimit --help`)?

```bash
asamarskii@asm-tst:~$ sysctl fs.nr_open
fs.nr_open = 1048576
```

Параметр обозначает максимальное количество файловых дескрипторов. Значение по умолчанию — 1024*1024 (1048576).

Данный лимит не позволит достичь значение soft ограничения (`ulimit -Sn`) равное 1024

#### 6. Запустите любой долгоживущий процесс (не `ls`, который отработает мгновенно, а, например, `sleep 1h`) в отдельном неймспейсе процессов; покажите, что ваш процесс работает под PID 1 через `nsenter`. Для простоты работайте в данном задании под root (`sudo -i`). Под обычным пользователем требуются дополнительные опции (`--map-root-user`) и т.д.

```bash
# Делаем форк оболочки в отдельный namespace
unshare -f --pid --mount-proc /bin/bash

# Узнаем PID созданного форка
ps aux | grep bash
e2sly4rz     990  0.0  0.2   8276  5296 pts/0    Ss   08:51   0:00 -bash
root        1031  0.0  0.2   8260  5320 pts/0    S    08:56   0:00 -bash
root        1062  0.0  0.0   5480   520 pts/0    S    08:57   0:00 unshare -f --pid --mount-proc /bin
bash
root        1063  0.0  0.1   7236  4012 pts/0    S+   08:57   0:00 /bin/bash
e2sly4rz    1175  0.0  0.2   8276  5264 pts/1    Ss   08:57   0:00 -bash
root        1186  0.0  0.2   8260  5312 pts/1    S    08:57   0:00 -bash
root        1308  0.0  0.0   6300   672 pts/1    S+   08:58   0:00 grep --color=auto bash

# Передаем команду ps в namespace форка
nsenter -t 1063 -p -m ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1   7236  4012 pts/0    S+   08:57   0:00 /bin/bash
root           8  0.0  0.1   8892  3272 pts/1    R+   08:59   0:00 ps aux
```

#### 7. Найдите информацию о том, что такое `:(){ :|:& };:`. Запустите эту команду в своей виртуальной машине Vagrant с Ubuntu 20.04 (**это важно, поведение в других ОС не проверялось**). Некоторое время все будет "плохо", после чего (минуты) – ОС должна стабилизироваться. Вызов `dmesg` расскажет, какой механизм помог автоматической стабилизации. Как настроен этот механизм по-умолчанию, и как изменить число процессов, которое можно создать в сессии?

Это однострочная запись функции fork bomb:

- :() — Определение функции с названием ":"
- {  — Открытие функции.
- :|: — загрузка копии функции в память тем самым, вызывая саму себя и передавая результат на другой вызов функции.
- & — Помещает вызов функции в фоновый режим, чтобы fork не мог «умереть», тем самым начиная есть системные ресурсы.
- } — Закрытие функции.
- ; — Разделитель.
- : — Запускает функцию которая порождает fork bomb().

Скорее всего стабилизирующим механизмом является Process Number Controller
[   37.397923] cgroup: fork rejected by pids controller in /user.slice/user-1000.slice/session-1.scope


Изменить количество процессов можно:
- В файле  `/etc/limits.conf` или `/etc/security/limits.conf`
- Командой `ulimit -u [кол-во процессов]`
