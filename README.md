# Домашнее задание к занятию  «Защита хоста - Евгений Борзов»

### Задание 1

1. Установите **eCryptfs**.
2. Добавьте пользователя cryptouser.
3. Зашифруйте домашний каталог пользователя с помощью eCryptfs.



sudo apt install ecryptfs-utils
sudo useradd -m cryptouser
sudo ls -Al /home/cryptouser
sudo cd /home
sudo mount -t ecryptfs cryptouser cryptouser
sudo umount cryptouser
sudo ls -Al /home/cryptouser



#sudo ecryptfs-migrate-home -u cryptouser

*as cryptouser:*
#ls /home/.ecryptfs/cryptouser/.Private
#ls ~

*You should see files with randomized, unreadable filenames. This confirms the data is encrypted.*
*Check your actual home directory (/home/targetuser) to ensure all your files are present and readable.*

#sudo rm -rf /home/cryptouser.XXXXXXXX



*В качестве ответа  пришлите снимки экрана домашнего каталога пользователя с исходными и зашифрованными данными.*  

### Задание 2

1. Установите поддержку **LUKS**.
2. Создайте небольшой раздел, например, 100 Мб.
3. Зашифруйте созданный раздел с помощью LUKS.


sudo apt install gparted cryptsetup

*create partition*

sudo cryptsetup -y -v --type luks2 luksFormat /dev/*sdb1*
sudo cryptsetup luksOpen /dev/sdv1 disk
ls /dev/mapper/disk
sudo dd if=/dev/zero of=/dev/mapper/disk
sudo mkfs.ext4 /dev/mapper/disk
mkdir .secret
sudo mount /dev/mapper/disk .secret
sudo umount .secret
sudo cryptsetup luksClose disk



*В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.*


## Дополнительные задания (со звёздочкой*)

Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале

### Задание 3 *

1. Установите **apparmor**.
2. Повторите эксперимент, указанный в лекции.
3. Отключите (удалите) apparmor.

sudo apt install apparmor-profiles apparmor-utils apparmor-profiles-extra
sudo cp /bin/ping /usr/bin/man
sudo man 127.0.0.1
sudo aa-enforce man
sudo man 127.0.0.1
sudo apparmor stop
sudo service apparmor teardown



*В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.*
