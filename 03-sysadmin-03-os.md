## Домашнее задание к занятию "3.3. Операционные системы, лекция 1"

##### 1. Какой системный вызов делает команда `cd`? В прошлом ДЗ мы выяснили, что `cd` не является самостоятельной программой, это shell builtin, поэтому запустить `strace` непосредственно на `cd` не получится. Тем не менее, вы можете запустить `strace` на `/bin/bash -c 'cd /tmp'`. В этом случае вы увидите полный список системных вызовов, которые делает сам bash при старте. Вам нужно найти тот единственный, который относится именно к `cd`.

```bash
chdir("/tmp")
```

##### 2. Попробуйте использовать команду `file` на объекты разных типов на файловой системе. Например:

```bash
vagrant@netology1:~$ file /dev/tty
/dev/tty: character special (5/0)
vagrant@netology1:~$ file /dev/sda
/dev/sda: block special (8/0)
vagrant@netology1:~$ file /bin/bash
/bin/bash: ELF 64-bit LSB shared object, x86-64
```

##### Используя `strace` выясните, где находится база данных `file` на основании которой она делает свои догадки.

```bash
# Согласно приоритету сначала проверяются пользовательские каталоги на наличие пользовательского файла
stat("/home/asamarskii/.magic.mgc", 0x7ffe42697210) = -1 ENOENT (No such file or directory)
stat("/home/asamarskii/.magic", 0x7ffe42697210) = -1 ENOENT (No such file or directory)

# Затем проверяются "стандартные" расположения на наличие файла
openat(AT_FDCWD, "/etc/magic.mgc", O_RDONLY) = -1 ENOENT (No such file or directory)
stat("/etc/magic", {st_mode=S_IFREG|0644, st_size=111, ...}) = 0
openat(AT_FDCWD, "/etc/magic", O_RDONLY) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=111, ...}) = 0
read(3, "# Magic local data for file(1) c"..., 4096) = 111
read(3, "", 4096)                       = 0
close(3)                                = 0

# Файл найден
openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3
```

##### 3. Предположим, приложение пишет лог в текстовый файл. Этот файл оказался удален (deleted в lsof), однако возможности сигналом сказать приложению переоткрыть файлы или просто перезапустить приложение – нет. Так как приложение продолжает писать в удаленный файл, место на диске постепенно заканчивается. Основываясь на знаниях о перенаправлении потоков предложите способ обнуления открытого удаленного файла (чтобы освободить место на файловой системе).

По-простому не получилось, пришлось делать так:

```bash
# Создаем отдельный дескриптор с перенаправлением (для наглядности)
e2sly4rz@ubuntu:~$ exec 5> /tmp/ping.md

# Запускаем логирование ping в файл
e2sly4rz@ubuntu:~$ ping 8.8.8.8 >&5

# Ищем PID процесса
e2sly4rz@ubuntu:~$ sudo lsof | grep ping.md
bash      1048                       e2sly4rz    5w      REG              253,0     1081     539668 /tmp/ping.md
ping      1187                       e2sly4rz    1w      REG              253,0     1081     539668 /tmp/ping.md
ping      1187                       e2sly4rz    5w      REG              253,0     1081     539668 /tmp/ping.md

# Видим, что файл постепенно растет в размере
e2sly4rz@ubuntu:~$ sudo lsof | grep ping.md
bash      1048                       e2sly4rz    5w      REG              253,0     1191     539668 /tmp/ping.md
ping      1187                       e2sly4rz    1w      REG              253,0     1191     539668 /tmp/ping.md
ping      1187                       e2sly4rz    5w      REG              253,0     1191     539668 /tmp/ping.md

# Удаляем файл
e2sly4rz@ubuntu:~$ rm /tmp/ping.md
e2sly4rz@ubuntu:~$ sudo lsof | grep ping.md
bash      1048                       e2sly4rz    5w      REG              253,0     1741     539668 /tmp/ping.md (deleted)
ping      1187                       e2sly4rz    1w      REG              253,0     1741     539668 /tmp/ping.md (deleted)
ping      1187                       e2sly4rz    5w      REG              253,0     1741     539668 /tmp/ping.md (deleted)

# Останавливаем ping т.к. команда судя по всему постоянно переписывает файл в полном объеме, но у нас есть "копия"
e2sly4rz@ubuntu:~$ sudo lsof | grep ping.md
bash      1048                       e2sly4rz    5w      REG              253,0     2168     539668 /tmp/ping.md (deleted)

# Обнуляем файл дескриптор
e2sly4rz@ubuntu:~$ cat /dev/null > /proc/1048/fd/5

# Проверяем результат
e2sly4rz@ubuntu:~$ sudo lsof | grep ping.md
bash      1048                       e2sly4rz    5w      REG              253,0        0     539668 /tmp/ping.md (deleted)
```

##### 4. Занимают ли зомби-процессы какие-то ресурсы в ОС (CPU, RAM, IO)?

Нет.
Зомби процессы - это завершившиеся процессы, которые ждут принятия их кода возврата.

##### 5. В iovisor BCC есть утилита opensnoop:

```bash
root@vagrant:~$ dpkg -L bpfcc-tools | grep sbin/opensnoop
/usr/sbin/opensnoop-bpfcc
```

##### На какие файлы вы увидели вызовы группы open за первую секунду работы утилиты? Воспользуйтесь пакетом bpfcc-tools для Ubuntu 20.04. Дополнительные сведения по установке.

```bash
asamarskii@asm-tst:~$ sudo opensnoop-bpfcc -d 1
PID    COMM               FD ERR PATH
8018   head                3   0 /etc/ld.so.cache
8018   head                3   0 /lib/x86_64-linux-gnu/libc.so.6
8018   head                3   0 /usr/lib/locale/locale-archive
8018   head                3   0 /usr/share/locale/locale.alias
8018   head               -1   2 /usr/share/locale/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale/ru_RU.utf8/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale/ru_RU/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale/ru.UTF-8/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale/ru.utf8/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale/ru/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale-langpack/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale-langpack/ru_RU.utf8/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale-langpack/ru_RU/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale-langpack/ru.UTF-8/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale-langpack/ru.utf8/LC_MESSAGES/coreutils.mo
8018   head               -1   2 /usr/share/locale-langpack/ru/LC_MESSAGES/coreutils.mo
8018   head                3   0 /proc/meminfo
8019   head                3   0 /etc/ld.so.cache
8019   head                3   0 /lib/x86_64-linux-gnu/libc.so.6
8019   head                3   0 /usr/lib/locale/locale-archive
8019   head                3   0 /usr/share/locale/locale.alias
8019   head               -1   2 /usr/share/locale/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale/ru_RU.utf8/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale/ru_RU/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale/ru.UTF-8/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale/ru.utf8/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale/ru/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale-langpack/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale-langpack/ru_RU.utf8/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale-langpack/ru_RU/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale-langpack/ru.UTF-8/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale-langpack/ru.utf8/LC_MESSAGES/coreutils.mo
8019   head               -1   2 /usr/share/locale-langpack/ru/LC_MESSAGES/coreutils.mo
8019   head                3   0 /proc/stat
8019   head                3   0 /proc/version
8019   head                3   0 /proc/uptime
8019   head                3   0 /proc/loadavg
8019   head                3   0 /proc/sys/fs/file-nr
8019   head                3   0 /proc/sys/kernel/hostname
8020   tail                3   0 /etc/ld.so.cache
8020   tail                3   0 /lib/x86_64-linux-gnu/libc.so.6
8020   tail                3   0 /usr/lib/locale/locale-archive
8020   tail                3   0 /usr/share/locale/locale.alias
8020   tail               -1   2 /usr/share/locale/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale/ru_RU.utf8/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale/ru_RU/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale/ru.UTF-8/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale/ru.utf8/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale/ru/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale-langpack/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale-langpack/ru_RU.utf8/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale-langpack/ru_RU/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale-langpack/ru.UTF-8/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale-langpack/ru.utf8/LC_MESSAGES/coreutils.mo
8020   tail               -1   2 /usr/share/locale-langpack/ru/LC_MESSAGES/coreutils.mo
8020   tail                3   0 /proc/net/dev
8021   df                  3   0 /etc/ld.so.cache
8021   df                  3   0 /lib/x86_64-linux-gnu/libc.so.6
8021   df                  3   0
8021   df                  3   0 /usr/share/locale/locale.alias
8021   df                 -1   2 /usr/share/locale/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale/ru_RU.utf8/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale/ru_RU/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale/ru.UTF-8/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale/ru.utf8/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale/ru/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale-langpack/ru_RU.UTF-8/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale-langpack/ru_RU.utf8/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale-langpack/ru_RU/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale-langpack/ru.UTF-8/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale-langpack/ru.utf8/LC_MESSAGES/coreutils.mo
8021   df                 -1   2 /usr/share/locale-langpack/ru/LC_MESSAGES/coreutils.mo
8021   df                  3   0 /proc/self/mountinfo
8021   df                  3   0 /usr/lib/x86_64-linux-gnu/gconv/gconv-modules.cache
8022   who                 3   0 /etc/ld.so.cache
8022   who                 3   0 /lib/x86_64-linux-gnu/libc.so.6
8022   who                 3   0 /usr/lib/locale/locale-archive
8022   who                 3   0 /var/run/utmp
8022   who                 3   0 /etc/localtime
8023   sleep               3   0 /etc/ld.so.cache
8023   sleep               3   0 /lib/x86_64-linux-gnu/libc.so.6
8023   sleep               3   0 /usr/lib/locale/locale-archive
1      systemd            12   0 /proc/651/cgroup
```

##### 6. Какой системный вызов использует uname -a? Приведите цитату из man по этому системному вызову, где описывается альтернативное местоположение в /proc, где можно узнать версию ядра и релиз ОС.

Команда использует одноименный системный вызов:

```bash
asamarskii@asm-tst:~$ strace uname -a
uname({sysname="Linux", nodename="asm-tst", ...}) = 0
fstat(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(0x88, 0), ...}) = 0
uname({sysname="Linux", nodename="asm-tst", ...}) = 0
uname({sysname="Linux", nodename="asm-tst", ...}) = 0
write(1, "Linux asm-tst 5.4.0-99-generic #"..., 106Linux asm-tst 5.4.0-99-generic #112-Ubuntu SMP Thu Feb 3 13:50:55 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
) = 106
close(1)                                = 0
close(2)                                = 0
exit_group(0)                           = ?
+++ exited with 0 +++
```

Цитата из `man 2 uname`:
> Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}.

##### 7. Чем отличается последовательность команд через ; и через && в bash? Например:

```bash
# Команды будут выполнены последовательно не зависимо от кода возврата.
root@netology1:~$ test -d /tmp/some_dir; echo Hi
Hi

# Команды будут выполнены последовательно.
# Выполнение следующей команды произойдет только при возврате успешного статуса предыдущей команды.
root@netology1:~$ test -d /tmp/some_dir && echo Hi
```

##### Есть ли смысл использовать в bash &&, если применить set -e?

`set -e` - завершит текущую сессию оболочки при ненулевом возврате одной из комманд за исключением комманд в составе операторов while, until, if, && и ||, кроме последней в списке.

Смысл есть т.к. поведение оболочки при && будет различаться.

##### 8. Из каких опций состоит режим bash set -euxo pipefail и почему его хорошо было бы использовать в сценариях?

- **errexit** - прекращает выполнение скрипта при ненулевом возврате одной из комманд за исключением комманд в составе операторов while, until, if, && и ||, кроме последней в списке.
- **nounset** -прекращает выполнение скрипта, если встретилась несуществующая переменная.
- **xtrace** - выводит выполняемые команды в stdout перед выполненинем.
- **pipefail** - прекращает выполнение скрипта, даже если одна из частей | завершилась ошибкой.

В целом, все опции полезны для безопасного дебага скрипта

##### 9. Используя -o stat для ps, определите, какой наиболее часто встречающийся статус у процессов в системе. В man ps ознакомьтесь (/PROCESS STATE CODES) что значат дополнительные к основной заглавной буквы статуса процессов. Его можно не учитывать при расчете (считать S, Ss или Ssl равнозначными).

Большинство процессов имеют статус:
- I< - высокоприоритетные системные процессы
- S  - в ожидании (прерывистый сон)
