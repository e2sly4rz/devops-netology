## 1. Какого типа команда `cd`? Попробуйте объяснить, почему она именно такого типа; опишите ход своих мыслей, если считаете что она могла бы быть другого типа.

```bash
vagrant@vagrant:~$ type cd
cd is a shell builtin
```

Перемещение по структуре каталогов в ОС это очевидная необходимость. Было бы странно если бы она не предусматривалась изначально именно как встроенная команда.

## 2. Какая альтернатива без pipe команде `grep <some_string> <some_file> | wc -l`? `man grep` поможет в ответе на этот вопрос. Ознакомьтесь с документом о других подобных некорректных вариантах использования pipe.

```bash
vagrant@vagrant:~/test$ cat test.txt
123
qwe
asd
zxc
123
qwe
asd
zxc
vagrant@vagrant:~/test$ grep 123 test.txt | wc -l
2
vagrant@vagrant:~/test$ grep 123 test.txt -c
2
```

## 3. Какой процесс с PID 1 является родителем для всех процессов в вашей виртуальной машине Ubuntu 20.04?

```bash
vagrant@vagrant:~/test$ pstree -p
systemd(1)─┬─VBoxService(809)─┬─{VBoxService}(810)
```

## 4. Как будет выглядеть команда, которая перенаправит вывод stderr ls на другую сессию терминала?

```bash
vagrant@vagrant:~/test$ who
vagrant tty1	2022-02-05 10:21
vagrant pts/0	2022-02-05 09:30 (10.0.2.2)
vagrant@vagrant:~/test$ touch /root/123 2>/dev/pts/0
```

```bash
vagrant@vagrant:~/test$ touch: cannot touch '/root/123': Permission denied
```

## 5. Получится ли одновременно передать команде файл на stdin и вывести ее stdout в другой файл? Приведите работающий пример.

```bash
vagrant@vagrant:~/test$ cat test.txt
123
qwe
asd
zxc
123
qwe
asd
zxc
vagrant@vagrant:~/test$ cat < test.txt > test2.txt
vagrant@vagrant:~/test$ cat test2.txt
123
qwe
asd
zxc
123
qwe
asd
zxc
```

## 6. Получится ли вывести находясь в графическом режиме данные из PTY в какой-либо из эмуляторов TTY? Сможете ли вы наблюдать выводимые данные?

Немного непонятно про какой графический режим идет речь, но данные между сессиями перенаправлять можно.

```bash
vagrant@vagrant:/dev$ who
vagrant  tty1         2022-02-05 10:21
vagrant  pts/0        2022-02-05 09:30 (10.0.2.2)
vagrant@vagrant:/dev$ echo hello > /dev/tty1
```

```bash
vagrant@vagrant:/dev$ echo hello > /dev/pts/0
```

## 7. Выполните команду `bash 5>&1`. К чему она приведет? Что будет, если вы выполните `echo netology > /proc/$$/fd/5`? Почему так происходит?

`bash 5>&1` - создаем новый файловый дескриптор с перенапрвлением на поток вывода

`echo netology > /proc/$$/fd/5` - команда `echo` "печатает" netology и направляет его на дескриптор 5 текущей сессии, который в свою очередь перенаправляет вывод на stdout (из-за команды `bash 5>&1`).

В результате видим вывод в консоли слово netology

## 8. Получится ли в качестве входного потока для pipe использовать только stderr команды, не потеряв при этом отображение stdout на pty? Напоминаем: по умолчанию через pipe передается только stdout команды слева от | на stdin команды справа. Это можно сделать, поменяв стандартные потоки местами через промежуточный новый дескриптор, который вы научились создавать в предыдущем вопросе.

Да

```bash
vagrant@vagrant: bash 5>&2
vagrant@vagrant:~$ (echo hello && cat 123.md) 2>&1 1>&5 | grep '..*' > /dev/tty1
hello
```

```bah
cat: 123.md: No such file or directory
```

## 9. Что выведет команда `cat /proc/$$/environ`? Как еще можно получить аналогичный по содержанию вывод?

Вывод переменных окружения аналогичный команде `env`

## 10. Используя man, опишите что доступно по адресам /proc/<PID>/cmdline, /proc/<PID>/exe.

1. Информация о процессе из командной строки
2. Символьная ссылка на исполняемый файл

## 11. Узнайте, какую наиболее старшую версию набора инструкций SSE поддерживает ваш процессор с помощью /proc/cpuinfo.

SSE 4.2

```bash
vagrant@vagrant:~$ grep sse /proc/cpuinfo
flags   : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq pni ssse3 cx16 pcid sse4_1 sse4_2 hypervisor lahf_lm invpcid_single pti fsgsbase invpcid md_clear flush_l1d arch_capabilities
flags   : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq pni ssse3 cx16 pcid sse4_1 sse4_2 hypervisor lahf_lm invpcid_single pti fsgsbase invpcid md_clear flush_l1d arch_capabilities
```

## 12. При открытии нового окна терминала и `vagrant ssh` создается новая сессия и выделяется pty. Это можно подтвердить командой tty, которая упоминалась в лекции 3.2. Однако:

```bash
vagrant@netology1:~$ ssh localhost 'tty'
not a tty
```

## Почитайте, почему так происходит, и как изменить поведение.

По умолчанию при запуске команды на удаленном компьютере с помощью ssh TTY не запускается для удаленного сеанса. Отсюда и ответ на команду.
Можно использовать опцию ssh -t для принудительного запуска TTY.

## 13. Бывает, что есть необходимость переместить запущенный процесс из одной сессии в другую. Попробуйте сделать это, воспользовавшись reptyr. Например, так можно перенести в screen процесс, который вы запустили по ошибке в обычной SSH-сессии.

- Для примера запускаем `top`
- "Сворачиваем" (CTRL-Z)
- Отправляем в фон `bg`
- Отвязываем процесс `disown top`
- Смотрим PID процесса `ps -a`
- Запускаем другой сеанс `tmux`
- Переподвязываем процесс на него `reptyr [нужный нам PID]`
- Отсоединяемся от tmux и отключаемся от ssh
- При повторном подключении по ssh может открыть tmux (`tmux attach`), процесс будет на месте.

## 14. `sudo echo string > /root/new_file` не даст выполнить перенаправление под обычным пользователем, так как перенаправлением занимается процесс shell'а, который запущен без sudo под вашим пользователем. Для решения данной проблемы можно использовать конструкцию `echo string | sudo tee /root/new_file`. Узнайте что делает команда `tee` и почему в отличие от `sudo echo` команда с `sudo tee` будет работать.

Команда `tee` читает stdin и пишет одновременно в stdout и файл.
`sudo echo` не сработает т.к. `echo` только занимается выводом как встроенная команда bash, а вот само перенаправление + запись делает как раз оболочка без привелегий.
в случае с `sudo tee` записью занимается именно `tee` запущенная с необходимыми для этого привилегиями.