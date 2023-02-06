# HW_Linux

# Курс по linux 

## Задание:

Используя команду cat, создать два файла с данными, а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя.

## Решение:
> Подключался к SSH.
> На macOS через visualBox все работает идеально 
```
The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
(base) iMac-iMacSON:~ imacson$ ssh -p 9022 gb@localhost
gb@localhost's password: 
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-58-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 обновлений может быть применено немедленно.

The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Last login: Fri Feb  3 21:40:12 2023 from 10.0.2.2
gb@gb-VirtualBox:~$ cat > test1
Какой то текст 
gb@gb-VirtualBox:~$ cat > test2
Какойто текст 2 
gb@gb-VirtualBox:~$ cat test1 test2 >>  testall
gb@gb-VirtualBox:~$ cat testall
Какой то текст
Какойто текст 2 
gb@gb-VirtualBox:~$ mv testall testall1
gb@gb-VirtualBox:~$ cat testalll
Какой то текст
Какойто текст 2 
gb@gb-VirtualBox:~$
```

- **Команда cat (описание)**

  Название команды - это сокращения от слова catenate. По сути, задача команды cat очень проста - она читает данные из файла или стандартного ввода и выводит их на экран. Это все, чем занимается утилита. Но с помощью ее опций и операторов перенаправления вывода можно сделать очень многое. Сначала рассмотрим синтаксис утилиты:

  **$ cat опции файл1 файл2 ...**

  Вы можете передать утилите несколько файлов и тогда их содержимое будет выведено поочередно, без разделителей. Опции позволяют очень сильно видоизменить вывод и сделать именно то, что вам нужно. Рассмотрим основные опции:

    - **b** - нумеровать только непустые строки;
    - **E** - показывать символ $ в конце каждой строки;
    - **n** - нумеровать все строки;
    - **s** - удалять пустые повторяющиеся строки;
    - **T** - отображать табуляции в виде ^I;
    - **h** - отобразить справку;
    - **v** - версия утилиты.


## Задание:
Создать директорию, переместить файл туда. Удалить все созданные в этом и предыдущем задании директории и файлы.

### Решение:

```
Переместить файл в директорию можно командой mv $FILENAME $DIRNAME. Удаляем все файлы командой rm -r находясь в директории практического занятия

gb@gb-VirtualBox:~$ mkdir test
gb@gb-VirtualBox:~$ mv test1 test2 testall1 test
gb@gb-VirtualBox:~$ rm -r test
```

## Задание:

Создать файл file1 и наполнить его произвольным содержимым.

### Решение:

```
gb@gb-VirtualBox:~$ cat > file1
gtgrthsrthb
```
> Выход control+D

### Скопировать его в file2.

```
gb@gb-VirtualBox:~$ cp file1 file2
gb@gb-VirtualBox:~$ cat file2
gtgrthsrthb
```
> Выход control+D


### Создать символическую ссылку file3 на file1.

```
gb@gb-VirtualBox:~$ ln -s file1 file3
```

### Создать жесткую ссылку file4 на file1.

```
gb@gb-VirtualBox:~$ ln file1 file4
```

### Посмотреть, какие **inode** у файлов.

```

gb@gb-VirtualBox:~$ ls -li
итого 48
408040 -rw-rw-r-- 2 gb   gb       12 фев  6 14:05  file1
408041 -rw-rw-r-- 1 gb   gb       12 фев  6 14:06  file2
408010 lrwxrwxrwx 1 gb   gb        5 фев  6 14:06  file3 -> file1
408040 -rw-rw-r-- 2 gb   gb       12 фев  6 14:05  file4
     1 drwxrwx--- 1 root vboxsf   64 янв 26 18:52  home
405833 drwx------ 3 gb   gb     4096 янв 26 17:06  snap
405895 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Видео
405892 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Документы
405889 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Загрузки
405894 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Изображения
405893 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Музыка
405891 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Общедоступные
405888 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06 'Рабочий стол'
405890 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Шаблоны
```

### Удалить file1.

```
gb@gb-VirtualBox:~$ rm file1
```

### Что стало с остальными созданными файлами?

```
gb@gb-VirtualBox:~$ ls -li
итого 44
408041 -rw-rw-r-- 1 gb   gb       12 фев  6 14:06  file2
408010 lrwxrwxrwx 1 gb   gb        5 фев  6 14:06  file3 -> file1
408040 -rw-rw-r-- 1 gb   gb       12 фев  6 14:05  file4
     1 drwxrwx--- 1 root vboxsf   64 янв 26 18:52  home
405833 drwx------ 3 gb   gb     4096 янв 26 17:06  snap
405895 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Видео
405892 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Документы
405889 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Загрузки
405894 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Изображения
405893 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Музыка
405891 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Общедоступные
405888 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06 'Рабочий стол'
405890 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Шаблоны
gb@gb-VirtualBox:~$
```

### Попробовать вывести их на экран.

```
gb@gb-VirtualBox:~$ cat file2
gtgrthsrthb

gb@gb-VirtualBox:~$ cat file3
cat: file3: Нет такого файла или каталога

gb@gb-VirtualBox:~$ cat file4
gtgrthsrthb
```

### Дать созданным файлам другие, произвольные имена.

```
gb@gb-VirtualBox:~$ mv file2 finalFile2
gb@gb-VirtualBox:~$ mv file3 finalFile3
gb@gb-VirtualBox:~$ mv file4 finalFile4
```

### Создать новую символическую ссылку.

```
gb@gb-VirtualBox:~$ ln -s finalFile2 file2Link
```

### Переместить ссылки в другую директорию.

```
gb@gb-VirtualBox:~$ mkdir test #создал директорию 
gb@gb-VirtualBox:~$ mv file2Link finalFile3 finalFile4 test #переметил туда файлы 
```

Результат:Текст команд, которые применялись при выполнении задания. Присылаем в формате текстового документа: задание и команды для решения (без вывода). Формат - PDF (один файл на все задания).
