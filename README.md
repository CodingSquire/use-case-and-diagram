# Lab-processes  
*lsblk* используется, чтобы узнать информацию о всех блочных устройствах, которыми являются разделы жестких дисков и других устройств хранения данных (оптических приводов, флэш-накопителей).  

```
daniil@daniil-VirtualBox:~/myfiles$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0    7:0    0  89,1M  1 loop /snap/core/8039
loop1    7:1    0  89,1M  1 loop /snap/core/8268
loop2    7:2    0  44,2M  1 loop /snap/gtk-common-themes/1353
loop3    7:3    0   3,7M  1 loop /snap/gnome-system-monitor/123
loop4    7:4    0  54,5M  1 loop /snap/core18/1265
loop5    7:5    0   956K  1 loop /snap/gnome-logs/81
loop6    7:6    0  42,8M  1 loop /snap/gtk-common-themes/1313
loop7    7:7    0   4,2M  1 loop /snap/gnome-calculator/544
loop8    7:8    0   156M  1 loop /snap/gnome-3-28-1804/91
loop9    7:9    0  54,6M  1 loop /snap/core18/1288
loop10   7:10   0  14,8M  1 loop /snap/gnome-characters/375
loop11   7:11   0   4,2M  1 loop /snap/gnome-calculator/501
loop12   7:12   0   3,7M  1 loop /snap/gnome-system-monitor/111
loop13   7:13   0  1008K  1 loop /snap/gnome-logs/61
loop14   7:14   0  14,8M  1 loop /snap/gnome-characters/367
loop15   7:15   0 156,7M  1 loop /snap/gnome-3-28-1804/110
sda      8:0    0    30G  0 disk 
└─sda1   8:1    0    30G  0 part /
sr0     11:0    1  1024M  0 rom 
```

*blkid* — это утилита командной строки для поиска / вывода атрибутов блочных устройств.  Это означает «Идентификация блока».  

```
daniil@daniil-VirtualBox:~$ sudo blkid
/dev/loop0: TYPE="squashfs"
/dev/loop1: TYPE="squashfs"
/dev/loop2: TYPE="squashfs"
/dev/loop3: TYPE="squashfs"
/dev/loop4: TYPE="squashfs"
/dev/loop5: TYPE="squashfs"
/dev/loop6: TYPE="squashfs"
/dev/loop7: TYPE="squashfs"
/dev/sda1: UUID="662b75eb-ad11-4535-8e4a-60e31b4f3cf9" TYPE="ext4" PARTUUID="e27b9353-01"
/dev/loop8: TYPE="squashfs"
/dev/loop9: TYPE="squashfs"
/dev/loop10: TYPE="squashfs"
/dev/loop11: TYPE="squashfs"
/dev/loop12: TYPE="squashfs"
/dev/loop13: TYPE="squashfs"
/dev/loop14: TYPE="squashfs"
/dev/loop15: TYPE="squashfs"
```

*fdisk* -- выводит информацию о блочных устройствах.  
-l, --list           показать данные в виде списка  
```
daniil@daniil-VirtualBox:~$ sudo fdisk -l 
Диск /dev/loop0: 89,1 MiB, 93429760 байт, 182480 секторов
Единицы: секторов по 1 * 512 = 512 байт
Размер сектора (логический/физический): 512 байт / 512 байт
Размер I/O (минимальный/оптимальный): 512 байт / 512 байт

Диск /dev/sda: 30 GiB, 32212254720 байт, 62914560 секторов
Единицы: секторов по 1 * 512 = 512 байт
Размер сектора (логический/физический): 512 байт / 512 байт
Размер I/O (минимальный/оптимальный): 512 байт / 512 байт
Тип метки диска: dos
Идентификатор диска: 0xe27b9353

Устр-во    Загрузочный начало    Конец  Секторы Размер Идентификатор Тип
/dev/sda1  *             2048 62912511 62910464    30G            83 Linux

Диск /dev/loop8: 156 MiB, 163614720 байт, 319560 секторов
Единицы: секторов по 1 * 512 = 512 байт
Размер сектора (логический/физический): 512 байт / 512 байт
Размер I/O (минимальный/оптимальный): 512 байт / 512 байт
```





*parted -l* - выводит список разделов на всех блочных устройств  

```
daniil@daniil-VirtualBox:~$ sudo parted -l 
Модель: ATA VBOX HARDDISK (scsi)
Диск /dev/sda: 32,2GB
Размер сектора (логич./физич.): 512B/512B
Таблица разделов: msdos
Флаги диска: 

Номер  Начало  Конец   Размер  Тип      Файловая система  Флаги
 1     1049kB  32,2GB  32,2GB  primary  ext4              загрузочный
```

**Какой размер дисков?**  
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0    30G  0 disk        диск  
└─sda1   8:1    0    30G  0 part /      раздел  
sr0     11:0    1  1024M  0 rom         память доступная только для чтения  
```


**Есть ли неразмеченное место на дисках?**  
Есть, *fdisk* показывает существующие разделы, он не показывает неразмеченное место.  
Можно увидеть, что sda заканчивается на 62910464 цилиндре, а всего их - 62914560  
```
Диск /dev/sda: 30 GiB, 32212254720 байт, 62914560 секторов
Единицы: секторов по 1 * 512 = 512 байт
Размер сектора (логический/физический): 512 байт / 512 байт
Размер I/O (минимальный/оптимальный): 512 байт / 512 байт
Тип метки диска: dos
Идентификатор диска: 0xe27b9353

Устр-во    Загрузочный начало    Конец  Секторы Размер Идентификатор Тип
/dev/sda1  *             2048 62912511 62910464    30G            83 Linux
```

**Какой размер партиций?** Размер 30G  
**Какая таблица партционирования используется?** Таблица разделов: msdos  
**Какой диск, партция или лвм том смонтированы в /** sda1 part /  


*df* (от disk free) — утилита в UNIX и UNIX-подобных системах, показывает список всех файловых систем по именам устройств, сообщает их размер, занятое и свободное пространство и точки монтирования.   
-h, --human-readable  
Отобразит размер в человеко-читаемом формате, добавив названия единиц (Kилобайт, Mегабайт, Гигабайт, Tерабайт).  
```
daniil@daniil-VirtualBox:~$ sudo df -h
Файл.система   Размер Использовано  Дост Использовано% Cмонтировано в
udev             972M            0  972M            0% /dev
tmpfs            200M         1,8M  198M            1% /run
/dev/sda1         30G          17G   12G           61% /
tmpfs            996M         152M  845M           16% /dev/shm
tmpfs            5,0M         4,0K  5,0M            1% /run/lock
tmpfs            996M            0  996M            0% /sys/fs/cgroup
/dev/loop0        90M          90M     0          100% /snap/core/8039
/dev/loop1        90M          90M     0          100% /snap/core/8268
/dev/loop2        45M          45M     0          100% /snap/gtk-common-themes/1353
/dev/loop3       3,8M         3,8M     0          100% /snap/gnome-system-monitor/123
/dev/loop4        55M          55M     0          100% /snap/core18/1265
/dev/loop5       1,0M         1,0M     0          100% /snap/gnome-logs/81
/dev/loop6        43M          43M     0          100% /snap/gtk-common-themes/1313
/dev/loop7       4,3M         4,3M     0          100% /snap/gnome-calculator/544
/dev/loop10       15M          15M     0          100% /snap/gnome-characters/375
/dev/loop9        55M          55M     0          100% /snap/core18/1288
/dev/loop8       157M         157M     0          100% /snap/gnome-3-28-1804/91
/dev/loop13      1,0M         1,0M     0          100% /snap/gnome-logs/61
/dev/loop12      3,8M         3,8M     0          100% /snap/gnome-system-monitor/111
/dev/loop11      4,3M         4,3M     0          100% /snap/gnome-calculator/501
/dev/loop14       15M          15M     0          100% /snap/gnome-characters/367
/dev/loop15      157M         157M     0          100% /snap/gnome-3-28-1804/110
tmpfs            200M          16K  200M            1% /run/user/121
tmpfs            200M          52K  200M            1% /run/user/1000
```
-i, --inodes  
Вместо информации о блоках выдаётся информация об использовании inode'ов в файловой системе.  

```
daniil@daniil-VirtualBox:~$ sudo df -i
Файл.система    Iнодов IИспользовано IСвободно IИспользовано% Cмонтировано в
udev            248815           456    248359             1% /dev
tmpfs           254845           862    253983             1% /run
/dev/sda1      1966080        350405   1615675            18% /
tmpfs           254845           125    254720             1% /dev/shm
tmpfs           254845             6    254839             1% /run/lock
tmpfs           254845            18    254827             1% /sys/fs/cgroup
/dev/loop0       12842         12842         0           100% /snap/core/8039
/dev/loop1       12842         12842         0           100% /snap/core/8268
/dev/loop2       41746         41746         0           100% /snap/gtk-common-themes/1353
/dev/loop3         733           733         0           100% /snap/gnome-system-monitor/123
/dev/loop4       10062         10062         0           100% /snap/core18/1265
/dev/loop5         354           354         0           100% /snap/gnome-logs/81
/dev/loop6       39455         39455         0           100% /snap/gtk-common-themes/1313
/dev/loop7        1577          1577         0           100% /snap/gnome-calculator/544
/dev/loop10        274           274         0           100% /snap/gnome-characters/375
/dev/loop9       10093         10093         0           100% /snap/core18/1288
/dev/loop8       27755         27755         0           100% /snap/gnome-3-28-1804/91
/dev/loop13        354           354         0           100% /snap/gnome-logs/61
/dev/loop12        733           733         0           100% /snap/gnome-system-monitor/111
/dev/loop11       1574          1574         0           100% /snap/gnome-calculator/501
/dev/loop14        271           271         0           100% /snap/gnome-characters/367
/dev/loop15      27755         27755         0           100% /snap/gnome-3-28-1804/110
tmpfs           254845            25    254820             1% /run/user/121
tmpfs           254845            39    254806             1% /run/user/1000
```

*mount* - монтирование файловой системы.

**Какая файловая система примонтирована в /**  

```
daniil@daniil-VirtualBox:~$ sudo df -h
Файл.система   Размер Использовано  Дост Использовано% Cмонтировано в
udev             972M            0  972M            0% /dev
tmpfs            200M         1,8M  198M            1% /run
/dev/sda1         30G          17G   12G           61% /
```

**С какими опциями примонтирована файловая система в /** mount -t squashfs -o loop  
-o, --options <список> список параметров монтирования через запятую  (с использованием устройства loopback)  
(-t, --type тип (squashfs) )  
  
**Какой размер файловой системы приментированной в /mnt/mai**  

```
Файл.система   Размер Использовано  Дост Использовано% Cмонтировано в
/dev/loop11      128K         128K     0          100% /mnt/mai
```

Для копирования различных двоичных данных используется утилита *dd* linux, которая просто выполняет копирование данных из одного места в другое на двоичном уровне. Она может скопировать CD/DVD диск, раздел на диске или даже целый жесткий диск.

$ dd if=источник_копирования of=место_назначения параметры
bs - указывает сколько байт читать и записывать за один раз;
count - скопировать указанное количество блоков, размер одного блока указывается в параметре bs;  

Команда *free* предоставляет информацию об использованной и неиспользованной памяти, а так же о разделе подкачки (swap).  
free -h удобный для чтения человеком формат с единицами измерения.  
```
daniil@daniil-VirtualBox:~$ sudo dd if=/dev/zero of=/dev/shm/mai bs=1M count=100
100+0 записей получено
100+0 записей отправлено
104857600 bytes (105 MB, 100 MiB) copied, 0,0619875 s, 1,7 GB/s
daniil@daniil-VirtualBox:~$ free -h
              всего        занято        свободно      общая  буф./врем.   доступно
Память:        1,9G        1,4G        129M        276M        448M        151M
Подкачка:        1,4G        1,3G        113M
daniil@daniil-VirtualBox:~$ sudo rm -f /dev/shm/mai
daniil@daniil-VirtualBox:~$ free -h
              всего        занято        свободно      общая  буф./врем.   доступно
Память:        1,9G        1,4G        245M        146M        321M        271M
Подкачка:        1,4G        1,3G        118M

```
**Что такое tmpfs**  
Tmpfs — временное файловое хранилище во многих Unix-подобных ОС. Предназначена для монтирования файловой системы, но размещается в ОЗУ(оперативную память) вместо физического диска. Подобная конструкция является RAM-диском(программная технология, позволяющая хранить данные в быстродействующей оперативной памяти как на блочном устройстве).  

**Какая часть памяти изменялась?**  
Занятая, свободная, буф./врем., доступная.

```
daniil@daniil-VirtualBox:~# free -h
               всего       занято        свободно      общая  буф./врем.   доступно
Память:        1,9G        1,4G          161M          186M   414M         244M
Подкачка:      1,4G        869M          556M
daniil@daniil-VirtualBox:~# rm -f /dev/shm/mai
daniil@daniil-VirtualBox:~# free -h
               всего       занято        свободно      общая  буф./врем.   доступно
Память:        1,9G        1,3G          244M          120M   391M         371M
Подкачка:      1,4G        846M          578M
```
**Процессы**  
*ps* опции  
*ps* опции | grep параметр  

*ps -eF*  
*ps rx*  
*ps -e --forest*  
*ps -efL*  

**Какие процессы в системе порождают дочерние процессы через fork**  

```
daniil@daniil-VirtualBox:~# ps --forest
  PID TTY          TIME CMD
 3083 pts/0    00:00:00 su
 3097 pts/0    00:00:00  \_ bash
 5570 pts/0    00:00:00      \_ ps
```
**Какие процессы в системе являются мультитредовыми**  
```
daniil@daniil-VirtualBox:~$ ps -efL
UID        PID  PPID   LWP  C NLWP STIME TTY          TIME CMD
systemd+   413     1   413  0    1 дек24 ?     00:00:03 /lib/systemd/systemd-resolved
root       466     1   466  0    1 дек24 ?     00:00:00 /usr/sbin/cron -f
root       468     1   468  0   14 дек24 ?     00:00:00 /usr/lib/snapd/snapd
root       468     1   852  0   14 дек24 ?     00:00:00 /usr/lib/snapd/snapd
root       468     1   855  0   14 дек24 ?     00:00:00 /usr/lib/snapd/snapd
root       557     1   575  0    3 дек24 ?     00:00:00 /usr/lib/policykit-1/polkitd --no-
root       634     1   634  0    2 дек24 ?     00:00:00 /usr/bin/python3 /usr/share/unatte
root       634     1   762  0    2 дек24 ?     00:00:00 /usr/bin/python3 /usr/share/unatte
root       643     1   643  0    9 дек24 ?     00:00:00 /usr/bin/containerd
```
LWP - показывает потоки процессора, где столбцы NLWP (количество потоков) и LWP (идентификатор потока).  

**команда**
ps axo rss | tail -n +2 | paste -sd+ | bc  
размер физической памяти | выведет все начиная со второй строчки | команда paste чтобы получить строки в одной с + в качестве разделителя: paste -sd+ | bc  
 
**Что подсчитывается этой командой** размер физической памяти занимаемая всеми процессами  
**Почему цифра такая странная** сложили  

*Smem* – это инструмент предоставления отчетов в командной строке, который выдает пользователю различные сводки по использованию памяти в системе Linux.   

```
  PID User     Command                         Swap      USS      PSS      RSS 
  986 root     bpfilter_umh                      84        4       13     1348 
  912 gdm      /usr/lib/gdm3/gdm-x-session      684        4       41     4856 
  714 kernoops /usr/sbin/kerneloops --test      340      152      214     2036 
 2095 daniil   /usr/bin/ssh-agent /usr/bin        0      340      345     1144 
```


```
 PID User     Command                         Swap      USS      PSS      RSS 
 3899 root     sudo python my_server.py           0     1408     1558     4252 
 3900 root     python my_server.py                0     4        51       1520 
```

**Убейте основной процесс kill -9 <pid>**  
**Какой PPID стал у первого чайлда**  

```
UID        PID  PPID  C STIME TTY          TIME CMD
daniil    1971     1  0 дек24 ?     00:00:00 /lib/systemd/systemd --user
root      3900  1971  0 дек24 pts/1 00:00:00 python my_server.py
```
**Проверьте текущий LA** load average: 0,56, 0,78, 0,73  
**Запишите top 3 процессов загружающих CPU**  
```
  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                  
 2136 daniil    20   0 3010232 141576  45340 S  3,0  6,9   7:08.88 gnome-shell              
 1991 daniil    20   0  478320  78808  40080 S  1,3  3,9   2:12.70 Xorg                     
 2515 daniil    20   0 3610484 444996  97592 S  1,3 21,8   3:36.62 firefox   
```


**Запишите top 3 процессов загружающих память**  

```
  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                  
 2515 daniil    20   0 3590080 461048  92268 S  1,3 22,6   3:51.23 firefox                  
 4925 daniil    20   0 3002824 279192 133540 S 11,5 13,7   1:04.96 Web Content              
 3600 daniil    20   0 2833368 197616  55032 S  1,0  9,7   0:33.28 Web Content  
```

```
**Запустите утилиту atop как сервис через systemd**  
ATOP - daniil-VirtualBox      2019/12/25  02:37:28      --------------        3h4m15s elapsed
PRC |  sys    6m10s   |  user  46m34s  |   #proc    230  |  #zombie    0  |   #exit      0  |
CPU |  sys       3%   |  user     27%  |   irq       0%  |  idle     69%  |   wait      1%  |
CPL |  avg1    0.56   |  avg5    0.58  |   avg15   0.61  |  csw 28602588  |   intr 6080791  |
MEM |  tot     1.9G   |  free  139.5M  |   cache 371.6M  |  buff   13.7M  |   slab  101.0M  |
SWP |  tot     1.4G   |  free  130.7M  |                 |  vmcom   7.5G  |   vmlim   2.4G  |
PAG |  scan 3928850   |  steal 1943e3  |   stall      0  |  swin  283276  |   swout 625067  |
DSK |           sda   |  busy      3%  |   read  446267  |  write 134938  |   avio 0.62 ms  |
NET |  transport      |  tcpi   84128  |   tcpo   72969  |  udpi   19868  |   udpo   20031  |
NET |  network        |  ipi   104226  |   ipo    89659  |  ipfrw      0  |   deliv 104223  |
NET |  enp0s3    0%   |  pcki  115331  |   pcko   78047  |  si   62 Kbps  |   so   14 Kbps  |
NET |  lo      ----   |  pcki   14880  |   pcko   14880  |  si    1 Kbps  |   so    1 Kbps  |
                        *** system and process activity since boot ***
  PID SYSCPU USRCPU   VGROW  RGROW   RDDSK  WRDSK  ST EXC   THR S  CPUNR  CPU CMD        1/11
 2136 33.63s 17m39s    2.9G 167.2M  453.7M  3872K  N-   -    10 R      0  10% gnome-shell
 2515 98.98s  8m44s    3.8G 365.2M    1.3G 771.7M  N-   -    63 S      0   6% firefox
 1991 55.13s  4m27s  464.7M 61224K  52028K    36K  N-   -     2 S      0   3% Xorg
 2702 27.82s  4m06s    2.8G 232.2M  175.6M     0K  N-   -    19 S      0   3% Web Content
 2672 32.14s  3m20s    3.0G 300.5M  276.2M     0K  N-   -    26 S      0   2% Web Content
 2728 26.30s  2m39s    3.0G 86216K  214.2M     0K  N-   -    24 S      0   2% Web Content
 7896  7.07s  1m55s    2.7G 141.5M  56920K   120K  N-   -    25 R      0   1% Web Content
 3600 10.79s 63.10s    2.7G 163.7M  81664K     0K  N-   -    23 S      0   1% Web Content
 2496  6.74s 28.67s  853.7M 17764K  42660K    32K  N-   -     4 S      0   0% gnome-terminal
 7822  4.35s 14.90s    2.5G 49064K  38560K     0K  N-   -    19 S      0   0% Web Content
 2563  2.62s 16.46s    2.5G 83320K  84328K     0K  N-   -    19 S      0   0% Web Content
 1628  1.16s 13.65s  446.8M  2680K  373.7M 218.7M  N-   -     3 S      0   0% packagekitd
   37 14.41s  0.00s      0K     0K      0K     0K  N-   -     1 S      0   0% kswapd0
 2156  2.06s  9.90s  369.4M  4508K   2140K     4K  N-   -     3 S      0   0% ibus-daemon
 1470  0.72s  9.85s    2.8G 40004K  113.2M     4K  N-   -    10 S      0   0% gnome-shell
  167  9.72s  0.00s      0K     0K      0K     0K  N-   -     1 I      0   0% kworker/0:1H-k
 2781  0.85s  6.35s    1.0G  7244K  44634K  2964K  N-   -     4 S      0   0% gnome-software
    1  4.32s  2.51s  220.5M  5576K  589.5M 23736K  N-   -     1 S      0   0% systemd
 5492  4.62s  1.97s  28000K 11016K   2164K   436K  N-   -     1 S      0   0% atop
  914  0.10s  6.10s  355.3M  3860K  37724K    76K  N-   -     2 S      0   0% Xorg
  468  3.80s  2.21s  667.9M 10768K  53757K  2000K  N-   -    14 S      0   0% snapd
```

**Запустите dd на генерацию файла размер в 3 гигабайта**  
**Удалите сгенеренный файл**  
```
daniil@daniil-VirtualBox:~/Рабочий стол$ sudo dd of=daniil bs=1 count=0 seek=3072M
0+0 записей получено
0+0 записей отправлено
0 bytes copied, 0,000304431 s, 0,0 kB/s
daniil@daniil-VirtualBox:~/Рабочий стол$ ls -lh | grep daniil
-rw-r--r-- 1 daniil daniil  895 окт 13 23:17 1.txt
drwxrwxr-x 2 daniil daniil 4,0K окт 20 21:40 arclab3
drwxr-xr-x 6 daniil daniil 4,0K дек  1 13:55 avito
-rw-rw-rw- 1 daniil daniil 1,2K окт 14 21:17 backup.txt
drwxr-xr-x 2 daniil daniil 4,0K сен 18 21:22 current
drwxr-xr-x 2 daniil daniil 4,0K сен 19 05:36 forecast
drwxrwxr-x 5 daniil daniil 4,0K дек 22 20:00 grpc
-rw-r--r-- 1 daniil daniil  673 дек  5 10:37 my_server.py
-rw-r--r-- 1 daniil daniil  33M дек 25 01:00 name-of-file
-rw-r--r-- 1 root   root   3,0G дек 25 01:01 daniil
drwxrwxrwx 8 daniil daniil 4,0K окт 15 01:44 start.avito
daniil@daniil-VirtualBox:~/Рабочий стол$ sudo rm daniil
daniil@daniil-VirtualBox:~/Рабочий стол$ ls -lh | grep daniil
-rw-r--r-- 1 daniil daniil  895 окт 13 23:17 1.txt
drwxrwxr-x 2 daniil daniil 4,0K окт 20 21:40 arclab3
drwxr-xr-x 6 daniil daniil 4,0K дек  1 13:55 avito
-rw-rw-rw- 1 daniil daniil 1,2K окт 14 21:17 backup.txt
drwxr-xr-x 2 daniil daniil 4,0K сен 18 21:22 current
drwxr-xr-x 2 daniil daniil 4,0K сен 19 05:36 forecast
drwxrwxr-x 5 daniil daniil 4,0K дек 22 20:00 grpc
-rw-r--r-- 1 daniil daniil  673 дек  5 10:37 my_server.py
-rw-r--r-- 1 daniil daniil  33M дек 25 01:00 name-of-file
drwxrwxrwx 8 daniil daniil 4,0K окт 15 01:44 start.avito
```

**Через atop скажите какой  pid был у процесса**  тот же что и pid сервиса  systemd  
**Проанализируйте нагрузку на диск через утилиты  iotop и iostat**  
*iotop* — утилита аналогична утилите top, но отображает использование не CPU и памяти, а работу процессов с дисками.  
```
Total DISK READ :       0.00 B/s | Total DISK WRITE :      59.53 K/s
Actual DISK READ:      11.16 K/s | Actual DISK WRITE:      18.60 K/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND                       
 8884 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.02 % [kworker/u2:1-ev~power_efficient]
 2604 be/4 daniil      0.00 B/s   59.53 K/s  0.00 %  0.00 % firefox -new-win~ [mozStorage #1]
    1 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % init splash
    2 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kthreadd]
    3 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_gp]
    4 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_par_gp]
    6 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kworker/0:0H-kblockd]
    8 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [mm_percpu_wq]
    9 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [ksoftirqd/0]
   10 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_sched]
   11 rt/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [migration/0]
   12 rt/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [idle_inject/0]
   14 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [cpuhp/0]
   15 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kdevtmpfs]
   16 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [netns]
   17 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_tasks_kthre]
   18 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kauditd]
   19 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [khungtaskd]
   20 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [oom_reaper]
   21 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [writeback]
```
*iostat* — утилита, предназначенная для мониторинга использования дисковых разделов, входящая в набор sysstat.  
```
daniil@daniil-VirtualBox:~$ sudo iostat
Linux 5.0.0-37-generic (daniil-VirtualBox) 	25.12.2019 	_x86_64_	(1 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          27,39    0,17    3,59    0,50    0,00   68,35

Device             tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
loop0             0,03         0,21         0,00       2325          0
loop1             6,20         6,37         0,00      70521          0
loop2             0,05         0,10         0,00       1158          0
loop3             0,01         0,02         0,00        231          0
loop4             0,02         0,08         0,00        844          0
loop5             0,00         0,01         0,00         95          0
loop6             0,05         0,10         0,00       1147          0
loop7             0,01         0,02         0,00        243          0
sda              52,73       615,34       395,16    6807369    4371588
loop8             0,04         0,22         0,00       2445          0
loop9             0,02         0,08         0,00        862          0
loop10            0,01         0,06         0,00        651          0
loop11            0,01         0,02         0,00        234          0
loop12            0,01         0,02         0,00        212          0
loop13            0,00         0,01         0,00         82          0
loop14            0,01         0,06         0,00        659          0
loop15            0,04         0,22         0,00       2480          0
loop16            0,00         0,00         0,00         39          0
```


