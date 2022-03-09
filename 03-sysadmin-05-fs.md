# Домашнее задание к занятию "3.5. Файловые системы"

#### 1. Узнайте о [sparse](https://ru.wikipedia.org/wiki/%D0%A0%D0%B0%D0%B7%D1%80%D0%B5%D0%B6%D1%91%D0%BD%D0%BD%D1%8B%D0%B9_%D1%84%D0%B0%D0%B9%D0%BB) (разряженных) файлах.

#### 2. Могут ли файлы, являющиеся жесткой ссылкой на один объект, иметь разные права доступа и владельца? Почему?

Нет.
Жесткая ссылка это фактически тот же файл, поэтому и права будут одинаковые.

Проверка:

```bash
# Создаем файл для проверки
asamarskii@asm-tst:~$ touch file1

# Создаем жесткую ссылку
asamarskii@asm-tst:~$ ln file1 hardlink

# Смотрим текущие права
asamarskii@asm-tst:~$ ls -l
total 4
-rw-rw-r-- 2 asamarskii asamarskii    0 фев 25 08:07 file1
-rw-rw-r-- 2 asamarskii asamarskii    0 фев 25 08:07 hardlink
drwxr-xr-x 3 asamarskii asamarskii 4096 фев 16 13:16 node_exporter-1.3.1.linux-amd64
-rw-rw-r-- 1 asamarskii asamarskii    0 фев 14 12:43 sudo

# Меняем права на оригинальном файле
asamarskii@asm-tst:~$ chmod 0755 file1

# Видим, что права меняются на оба файла
asamarskii@asm-tst:~$ ls -l
total 4
-rwxr-xr-x 2 asamarskii asamarskii    0 фев 25 08:07 file1
-rwxr-xr-x 2 asamarskii asamarskii    0 фев 25 08:07 hardlink
drwxr-xr-x 3 asamarskii asamarskii 4096 фев 16 13:16 node_exporter-1.3.1.linux-amd64
-rw-rw-r-- 1 asamarskii asamarskii    0 фев 14 12:43 sudo
```

#### 3. Сделайте `vagrant destroy` на имеющийся инстанс Ubuntu. Замените содержимое Vagrantfile следующим:

    ```bash
    Vagrant.configure("2") do |config|
      config.vm.box = "bento/ubuntu-20.04"
      config.vm.provider :virtualbox do |vb|
        lvm_experiments_disk0_path = "/tmp/lvm_experiments_disk0.vmdk"
        lvm_experiments_disk1_path = "/tmp/lvm_experiments_disk1.vmdk"
        vb.customize ['createmedium', '--filename', lvm_experiments_disk0_path, '--size', 2560]
        vb.customize ['createmedium', '--filename', lvm_experiments_disk1_path, '--size', 2560]
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk0_path]
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk1_path]
      end
    end
    ```

    Данная конфигурация создаст новую виртуальную машину с двумя дополнительными неразмеченными дисками по 2.5 Гб.

**Сделано**

```bash
e2sly4rz@netology:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0                       7:0    0 55,4M  1 loop /snap/core18/2128
loop1                       7:1    0 70,3M  1 loop /snap/lxd/21029
loop2                       7:2    0 32,3M  1 loop /snap/snapd/12704
sda                         8:0    0   32G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1,5G  0 part /boot
└─sda3                      8:3    0 30,5G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0 15,3G  0 lvm  /
sdb                         8:16   0  2,5G  0 disk
sdc                         8:32   0  2,5G  0 disk
sr0                        11:0    1 1024M  0 rom
```

#### 4. Используя `fdisk`, разбейте первый диск на 2 раздела: 2 Гб, оставшееся пространство.

```bash
# Запускаем fdisk на первом диске
e2sly4rz@netology:~$ sudo fdisk /dev/sdb

# Создаем таблицу GPT
Command (m for help): g
Created a new GPT disklabel (GUID: 7295CEB9-D258-3342-9AD9-6809A520697C).

# Разбиваем разделы согласно ДЗ
Command (m for help): n
Partition number (1-128, default 1):
First sector (2048-5242846, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-5242846, default 5242846): +2G

Created a new partition 1 of type 'Linux filesystem' and of size 2 GiB.

Command (m for help): n
Partition number (2-128, default 2):
First sector (4196352-5242846, default 4196352):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (4196352-5242846, default 5242846):

Created a new partition 2 of type 'Linux filesystem' and of size 511 MiB.

# Сохраняем результат и выходим из fdisk
Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

# Проверяем
e2sly4rz@netology:~$ sudo lsblk | grep sdb
sdb                         8:16   0  2,5G  0 disk
├─sdb1                      8:17   0    2G  0 part
└─sdb2                      8:18   0  511M  0 part
```

#### 5. Используя `sfdisk`, перенесите данную таблицу разделов на второй диск.

```bash
e2sly4rz@netology:~$ sudo sfdisk -d /dev/sdb | sudo sfdisk /dev/sdc
Checking that no-one is using this disk right now ... OK

Disk /dev/sdc: 2,51 GiB, 2684354560 bytes, 5242880 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Created a new GPT disklabel (GUID: 7295CEB9-D258-3342-9AD9-6809A520697C).
/dev/sdc1: Created a new partition 1 of type 'Linux filesystem' and of size 2 GiB.
/dev/sdc2: Created a new partition 2 of type 'Linux filesystem' and of size 511 MiB.
/dev/sdc3: Done.

New situation:
Disklabel type: gpt
Disk identifier: 7295CEB9-D258-3342-9AD9-6809A520697C

Device       Start     End Sectors  Size Type
/dev/sdc1     2048 4196351 4194304    2G Linux filesystem
/dev/sdc2  4196352 5242846 1046495  511M Linux filesystem

The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

#### 6. Соберите `mdadm` RAID1 на паре разделов 2 Гб.

```bash
# Создаем RAID1
e2sly4rz@netology:~$ sudo mdadm --create /dev/md/raid1 -l 1 -n 2 /dev/sd{b,c}1
mdadm: Note: this array has metadata at the start and
    may not be suitable as a boot device.  If you plan to
    store '/boot' on this device please ensure that
    your boot-loader understands md/v1.x metadata, or use
    --metadata=0.90
Continue creating array? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md/raid1 started.

# Проверяем
e2sly4rz@netology:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 55,4M  1 loop  /snap/core18/2128
loop1                       7:1    0 70,3M  1 loop  /snap/lxd/21029
loop2                       7:2    0 32,3M  1 loop  /snap/snapd/12704
sda                         8:0    0   32G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1,5G  0 part  /boot
└─sda3                      8:3    0 30,5G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0 15,3G  0 lvm   /
sdb                         8:16   0  2,5G  0 disk
├─sdb1                      8:17   0    2G  0 part
│ └─md127                   9:127  0    2G  0 raid1
└─sdb2                      8:18   0  511M  0 part
sdc                         8:32   0  2,5G  0 disk
├─sdc1                      8:33   0    2G  0 part
│ └─md127                   9:127  0    2G  0 raid1
└─sdc2                      8:34   0  511M  0 part
sr0                        11:0    1 1024M  0 rom
```

#### 7. Соберите `mdadm` RAID0 на второй паре маленьких разделов.

```bash
# Создаем RAID0
e2sly4rz@netology:~$ sudo mdadm --create /dev/md/raid0 -l 0 -n 2 /dev/sd{b,c}2
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md/raid0 started.

# Проверяем
e2sly4rz@netology:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 55,4M  1 loop  /snap/core18/2128
loop1                       7:1    0 70,3M  1 loop  /snap/lxd/21029
loop2                       7:2    0 32,3M  1 loop  /snap/snapd/12704
sda                         8:0    0   32G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1,5G  0 part  /boot
└─sda3                      8:3    0 30,5G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0 15,3G  0 lvm   /
sdb                         8:16   0  2,5G  0 disk
├─sdb1                      8:17   0    2G  0 part
│ └─md127                   9:127  0    2G  0 raid1
└─sdb2                      8:18   0  511M  0 part
  └─md126                   9:126  0 1017M  0 raid0
sdc                         8:32   0  2,5G  0 disk
├─sdc1                      8:33   0    2G  0 part
│ └─md127                   9:127  0    2G  0 raid1
└─sdc2                      8:34   0  511M  0 part
  └─md126                   9:126  0 1017M  0 raid0
sr0                        11:0    1 1024M  0 rom
```

#### 8. Создайте 2 независимых PV на получившихся md-устройствах.

```bash
e2sly4rz@netology:~$ sudo pvcreate /dev/md126 /dev/md127
  Physical volume "/dev/md126" successfully created.
  Physical volume "/dev/md127" successfully created.
  ```

#### 9. Создайте общую volume-group на этих двух PV.

```bash
e2sly4rz@netology:~$ sudo vgcreate vg1 /dev/md126 /dev/md127
  Volume group "vg1" successfully created
```

#### 10. Создайте LV размером 100 Мб, указав его расположение на PV с RAID0.

```bash
e2sly4rz@netology:$ sudo lvcreate -L 100M vg1 /dev/md126
  Logical volume "lvol0" created.
```

#### 11. Создайте `mkfs.ext4` ФС на получившемся LV.

```bash
e2sly4rz@netology:$ sudo mkfs.ext4 /dev/vg1/lvol0
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done
Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done
```

#### 12. Смонтируйте этот раздел в любую директорию, например, `/tmp/new`.

```bash
e2sly4rz@netology:~$ mkdir /tmp/new
e2sly4rz@netology:~$ sudo mount /dev/vg1/lvol0 /tmp/new/
```

#### 13. Поместите туда тестовый файл, например `wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz`.

```bash
e2sly4rz@netology:/tmp/new$ sudo wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz
e2sly4rz@netology:/tmp/new$ ls
lost+found  test.gz
```

#### 14. Прикрепите вывод `lsblk`.

```bash
e2sly4rz@netology:$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 55,4M  1 loop  /snap/core18/2128
loop1                       7:1    0 70,3M  1 loop  /snap/lxd/21029
loop3                       7:3    0 55,5M  1 loop  /snap/core18/2284
loop4                       7:4    0 43,6M  1 loop  /snap/snapd/14978
loop5                       7:5    0 61,9M  1 loop  /snap/core20/1361
loop6                       7:6    0 67,9M  1 loop  /snap/lxd/22526
sda                         8:0    0   32G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1,5G  0 part  /boot
└─sda3                      8:3    0 30,5G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0 15,3G  0 lvm   /
sdb                         8:16   0  2,5G  0 disk
├─sdb1                      8:17   0    2G  0 part
│ └─md127                   9:127  0    2G  0 raid1
└─sdb2                      8:18   0  511M  0 part
  └─md126                   9:126  0 1017M  0 raid0
    └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
sdc                         8:32   0  2,5G  0 disk
├─sdc1                      8:33   0    2G  0 part
│ └─md127                   9:127  0    2G  0 raid1
└─sdc2                      8:34   0  511M  0 part
  └─md126                   9:126  0 1017M  0 raid0
    └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
sr0                        11:0    1 1024M  0 rom
```

#### 15. Протестируйте целостность файла:

```bash
e2sly4rz@netology:/tmp/new$ gzip -t /tmp/new/test.gz && echo $?
0
```

#### 16. Используя pvmove, переместите содержимое PV с RAID0 на RAID1.

```bash
e2sly4rz@netology:$ sudo pvmove /dev/md/raid0 /dev/md/raid1
  /dev/md/raid0: Moved: 12,00%
  /dev/md/raid0: Moved: 100,00%
```

#### 17. Сделайте `--fail` на устройство в вашем RAID1 md.

```bash
e2sly4rz@netology:~$ sudo mdadm /dev/md127 --fail /dev/sdb1
mdadm: set /dev/sdb1 faulty in /dev/md127
```

#### 18. Подтвердите выводом `dmesg`, что RAID1 работает в деградированном состоянии.

```bash
e2sly4rz@netology:~$ sudo dmesg | grep md127
[ 3228.944369] md/raid1:md127: not clean -- starting background reconstruction
[ 3228.944371] md/raid1:md127: active with 2 out of 2 mirrors
[ 3228.944384] md127: detected capacity change from 0 to 2144337920
[ 3228.944896] md: resync of RAID array md127
[ 3239.466327] md: md127: resync done.
[763549.198278] md: data-check of RAID array md127
[763560.280907] md: md127: data-check done.
[1028942.884239] md/raid1:md127: Disk failure on sdb1, disabling device.
                 md/raid1:md127: Operation continuing on 1 devices.
```

#### 19. Протестируйте целостность файла, несмотря на "сбойный" диск он должен продолжать быть доступен:

    ```bash
    e2sly4rz@netology:~$ gzip -t /tmp/new/test.gz && echo $?
    0
    ```

#### 20. Погасите тестовый хост, `vagrant destroy`.
