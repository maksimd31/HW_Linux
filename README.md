# HomeWork#3

****Урок 3. Права доступа и безопасность****

Задание:

1. Создать два произвольных файла. 
    
    Первому присвоить права на чтение и запись для владельца и группы, только на чтение — для всех. 
    
    Второму присвоить права на чтение и запись только для владельца. 
    
    Сделать это в численном и символьном виде.
    

```
gb@gb-VirtualBox:~$ mkdir testHomeWork3 #создал директорию 
*Создать два произвольных файла.*
**echo "Запись в строку" файл.txt** 
gb@gb-VirtualBox:~/testHomeWork3$ **echo "какой-то текст"> file1.txt** #создал файл 
gb@gb-VirtualBox:~/testHomeWork3$ **echo "Еще какой-то текст"> file2.txt**

gb@gb-VirtualBox:~/testHomeWork3$ **ls -li**
итого 8
406356 -rw-rw-r-- 1 gb gb 24 фев  7 18:03 file1.txt
406358 -rw-rw-r-- 1 gb gb 31 фев  7 18:05 file2.txt

*#Владелец можкт читать писать. Группа и другие могут только читать.* 
gb@gb-VirtualBox:~/testHomeWork3$ **chmod 644 file1.txt** #В численом виде 
gb@gb-VirtualBox:~/testHomeWork3$ **chmod ugo=r file2.txt** #В символьном виде.
gb@gb-VirtualBox:~/testHomeWork3$ **chmod ug+w file2.txt** #В символьном виде.

*Второму присвоить права на чтение и запись только для владельца*
gb@gb-VirtualBox:~/testHomeWork3$ **chmod 600 file2.txt** #В численом виде 
gb@gb-VirtualBox:~/testHomeWork3$ **chmod ugo-rwx file2.txt** #В символьном виде.
gb@gb-VirtualBox:~/testHomeWork3$ **chmod u=rw file2.txt** #В символьном виде.
```

1. Назначить новых владельца и группу для директории целиком.

```
gb@gb-VirtualBox:~/testHomeWork3$ **chown gb  --recursive ~/testHomeWork3/file1.txt**
```

1. Управление пользователями:a. создать пользователя, используя утилиту useradd и adduser; удалить пользователя, используя утилиту userdel.

```
*Создаем пользоателя с помощью **usearadd***
gb@gb-VirtualBox:~/testHomeWork3$ **sudo useradd pupkin1** #Создаем пользоателя 

*Создаем пользоателя с помощью **adduser***
gb@gb-VirtualBox:~/testHomeWork3$ **sudo adduser pupkin2**
Добавляется пользователь «pupkin2» ...
Добавляется новая группа «pupkin2» (1002) ...
Добавляется новый пользователь «pupkin2» (1002) в группу «pupkin2» ...
Создаётся домашний каталог «/home/pupkin2» ...
Копирование файлов из «/etc/skel» ...
Новый пароль: 
НЕУДАЧНЫЙ ПАРОЛЬ: Пароль должен содержать не менее 8 символов
Повторите ввод нового пароля: 
Извините, но пароли не совпадают.
Новый пароль: 
НЕУДАЧНЫЙ ПАРОЛЬ: Пароль должен содержать не менее 8 символов
Повторите ввод нового пароля: 
passwd: пароль успешно обновлён
Изменение информации о пользователе pupkin2
Введите новое значение или нажмите ENTER для выбора значения по умолчанию
	Полное имя []: Pupok
	Номер комнаты []: 123
	Рабочий телефон []: 123
	Домашний телефон []: 123
	Другое []: pupkin
Данная информация корректна? [Y/n] y
*Удаляем принудительно c помощью **userdel***
gb@gb-VirtualBox:~/testHomeWork3$ **sudo userdel  --force pupkin1** 
```

1. Управление группами:a. создать группу с использованием утилит groupadd и addgroup попрактиковаться в смене групп у пользователей
    
    добавить пользователя в группу, не меняя основной;
    
2. Создать пользователя с правами суперпользователя. Сделать так, чтобы sudo не требовал пароль для выполнения команд.

```
gb@gb-VirtualBox:~/testHomeWork3$ **sudo groupadd groupStudent**

gb@gb-VirtualBox:~/testHomeWork3$ **cat /etc/group | grep groupStudent**
groupStudent:x:1003: #проверка

gb@gb-VirtualBox:~/testHomeWork3$ **sudo apt-get install addgroup**
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
E: Невозможно найти пакет addgroup
gb@gb-VirtualBox:~/testHomeWork3$

gb@gb-VirtualBox:~/testHomeWork3$ **sudo addgroup groupname**
Добавляется группа «groupname» (GID 1001) ...
Готово.
gb@gb-VirtualBox:~/testHomeWork3$

*Добавить пользователя в группу, не меняя основной*
gb@gb-VirtualBox:~/testHomeWork3$ **sudo usermod -a -G groupname pupkin2**

gb@gb-VirtualBox:~/testHomeWork3$ **sudo adduser sammy**
Добавляется пользователь «sammy» ...
Добавляется новая группа «sammy» (1005) ...
Добавляется новый пользователь «sammy» (1001) в группу «sammy» ...
Создаётся домашний каталог «/home/sammy» ...
Копирование файлов из «/etc/skel» ...
Новый пароль: 
НЕУДАЧНЫЙ ПАРОЛЬ: Пароль должен содержать не менее 8 символов
Повторите ввод нового пароля: 
passwd: пароль успешно обновлён
Изменение информации о пользователе sammy
Введите новое значение или нажмите ENTER для выбора значения по умолчанию
	Полное имя []: PupkinSuper
	Номер комнаты []: 123
	Рабочий телефон []: 123
	Домашний телефон []: 123
	Другое []: 123
Данная информация корректна? [Y/n] y

*Создать пользователя с правами суперпользователя. 
Сделать так, чтобы sudo не требовал пароль для выполнения команд.*

gb@gb-VirtualBox:~$ **sudo usermod -aG sudo sammy**
gb@gb-VirtualBox:~/testHomeWork3$ **su - sammy**
Пароль: 
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

sammy@gb-VirtualBox:~$ **sudo ls -la /root**
итого 24
drwx------  4 root root 4096 янв 26 17:06 .
drwxr-xr-x 20 root root 4096 янв 26 16:59 ..
-rw-r--r--  1 root root 3106 окт 15  2021 .bashrc
drwx------  2 root root 4096 авг  9 14:51 .cache
-rw-r--r--  1 root root  161 июл  9  2019 .profile
drwx------  5 root root 4096 янв 26 17:06 snap
sammy@gb-VirtualBox:~$
```
