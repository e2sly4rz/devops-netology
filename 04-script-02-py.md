# Домашнее задание к занятию "4.2. Использование Python для решения типовых DevOps задач"

## Обязательная задача 1

Есть скрипт:
```python
#!/usr/bin/env python3
a = 1
b = '2'
c = a + b
```

### Вопросы:
| Вопрос  | Ответ |
| ------------- | ------------- |
| Какое значение будет присвоено переменной `c`?  | Скрипт завершится ошибкой т.к. невозможно выполнить сложение int и str |
| Как получить для переменной `c` значение 12?  | Взять в кавычки значение `a` |
| Как получить для переменной `c` значение 3?  | Убрать кавычки у значения `b` |

## Обязательная задача 2
Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений. Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся. Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?

```python
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print("~/netology/sysadm-homeworks" prepare_result)
        break
```

### Ваш скрипт:
```python
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print("~/netology/sysadm-homeworks/",prepare_result)
```

### Вывод скрипта при запуске при тестировании:

```bash
asm@DESKTOP-43OOABH:~/netology$ ./test.py
~/netology/sysadm-homeworks/ folder/folder.txt
~/netology/sysadm-homeworks/ newfile.txt
~/netology/sysadm-homeworks/ readme.md
```

## Обязательная задача 3
1. Доработать скрипт выше так, чтобы он мог проверять не только локальный репозиторий в текущей директории, а также умел воспринимать путь к репозиторию, который мы передаём как входной параметр. Мы точно знаем, что начальство коварное и будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.

### Ваш скрипт:
```python
#!/usr/bin/env python3

import os
import sys

if len(sys.argv) > 1 and not os.path.isdir(sys.argv[1]):
    sys.exit('Не найдено. Проверьте путь: ' + sys.argv[1])

git_path = sys.argv[1] if len(sys.argv) > 1 else os.getcwd()
print('Git репозиторий: ' + git_path)
bash_command = ["cd " + git_path, 'git status']
result_os = os.popen(' && '.join(bash_command)).read()

for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(git_path + '/' + prepare_result)
```

### Вывод скрипта при запуске при тестировании:
```bash
asm@DESKTOP-43OOABH:~/netology$ ./test.py ./sysadm-homeworks
Git репозиторий: ./sysadm-homeworks
./sysadm-homeworks/folder/folder.txt
./sysadm-homeworks/newfile.txt
./sysadm-homeworks/readme.md

asm@DESKTOP-43OOABH:~/netology/sysadm-homeworks$ ../test.py
Git репозиторий: /home/asm/netology/sysadm-homeworks
/home/asm/netology/sysadm-homeworks/folder/folder.txt
/home/asm/netology/sysadm-homeworks/newfile.txt
/home/asm/netology/sysadm-homeworks/readme.md
```

## Обязательная задача 4
1. Наша команда разрабатывает несколько веб-сервисов, доступных по http. Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. Проблема в том, что отдел, занимающийся нашей инфраструктурой очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS имена. Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: `drive.google.com`, `mail.google.com`, `google.com`.

### Ваш скрипт:
```python
#!/usr/bin/env python3

import socket
import time

dns_list = ['drive.google.com', 'mail.google.com', 'google.com']
ip_list = [None, None, None]

while True:

    for i in range(0, len(dns_list)):
        time.sleep(1)
        ip = socket.gethostbyname(dns_list[i])
        print(dns_list[i] + ' -> ' + ip)
        if ip_list[i] is None:
            ip_list[i] = ip
        elif ip_list[i] != ip:
            print(dns_list[i] + ' IP changed from: ' + ip_list[i] + ' to: ' + ip)
```

### Вывод скрипта при запуске при тестировании:
```bash
asm@DESKTOP-43OOABH:~/netology$ ./test.py
drive.google.com -> 64.233.162.194
mail.google.com -> 173.194.222.83
google.com -> 74.125.131.113
```
