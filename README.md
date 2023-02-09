# HomeWork#4

# **Операционные системы и виртуализация (Linux) (семинары)**

### **Урок 4.**

**Подключение сторонних репозиториев, ручная установка пакетов**

Задание: 1. Подключить дополнительный репозиторий на выбор: Docker, Nginx , Oracle MySQL. Установить любой пакет из этого репозитория.

```
Nginx
gb@gb-VirtualBox:~$ **sudo apt install curl gnupg2 ca-certificates lsb-release ubuntu-keyring**
[sudo] пароль для gb: 
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
Уже установлен пакет lsb-release самой новой версии (11.1.0ubuntu4).
Уже установлен пакет ubuntu-keyring самой новой версии (2021.03.26).
ubuntu-keyring помечен как установленный вручную.
Уже установлен пакет ca-certificates самой новой версии (20211016ubuntu0.22.04.1).
Уже установлен пакет curl самой новой версии (7.81.0-1ubuntu1.7).
Следующие пакеты устанавливались автоматически и больше не требуются:
  libflashrom1 libftdi1-2
Для их удаления используйте «sudo apt autoremove».
Следующие НОВЫЕ пакеты будут установлены:
  gnupg2
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 44 пакетов не обновлено.
Необходимо скачать 5 548 B архивов.
После данной операции объём занятого дискового пространства возрастёт на 52,2 kB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 gnupg2 all 2.2.27-3ubuntu2.1 [5 548 B]
Получено 5 548 B за 0с (68,4 kB/s)
Выбор ранее не выбранного пакета gnupg2.
(Чтение базы данных … на данный момент установлено 187449 файлов и каталогов.)
Подготовка к распаковке …/gnupg2_2.2.27-3ubuntu2.1_all.deb …
Распаковывается gnupg2 (2.2.27-3ubuntu2.1) …
Настраивается пакет gnupg2 (2.2.27-3ubuntu2.1) …
Обрабатываются триггеры для man-db (2.10.2-1) …
gb@gb-VirtualBox:~$ curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
    | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1561  100  1561    0     0   3452      0 --:--:-- --:--:-- --:--:--  3445
gb@gb-VirtualBox:~$ gpg --dry-run --quiet --no-keyring --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg
pub   rsa2048 2011-08-19 [SC] [годен до: 2024-06-14]
      573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
uid                      nginx signing key <signing-key@nginx.com>

gb@gb-VirtualBox:~$ **echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list**
deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] http://nginx.org/packages/ubuntu jammy nginx
gb@gb-VirtualBox:~$ echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
http://nginx.org/packages/mainline/ubuntu `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] http://nginx.org/packages/mainline/ubuntu jammy nginx
gb@gb-VirtualBox:~$ sudo apt update
sudo apt install nginx
Сущ:1 http://ru.archive.ubuntu.com/ubuntu jammy InRelease
Пол:2 http://ru.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]                                              
Пол:3 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]                                               
Сущ:4 https://download.docker.com/linux/ubuntu jammy InRelease                                                          
Пол:5 http://ru.archive.ubuntu.com/ubuntu jammy-backports InRelease [107 kB]                                            
Игн:6 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy InRelease                                             
Пол:7 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [874 kB]
Ошб:8 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release                            
  404  Not Found [IP: 185.125.190.52 443]
Пол:9 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 DEP-11 Metadata [101 kB]          
Пол:10 http://ru.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 DEP-11 Metadata [265 kB]      
Пол:11 http://ru.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 DEP-11 Metadata [940 B]                   
Пол:12 http://ru.archive.ubuntu.com/ubuntu jammy-backports/main amd64 DEP-11 Metadata [7 980 B]                     
Пол:13 http://ru.archive.ubuntu.com/ubuntu jammy-backports/universe amd64 DEP-11 Metadata [12,4 kB]                     
Пол:14 http://nginx.org/packages/mainline/ubuntu jammy InRelease [3 587 B]                                             
Пол:15 http://nginx.org/packages/mainline/ubuntu jammy/nginx amd64 Packages [13,3 kB]
Чтение списков пакетов… Готово             
E: Репозиторий «https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release» не содержит файла Release.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).
N: Пропускается получение настроенного файла «nginx/binary-i386/Packages», так как репозиторий «http://nginx.org/packages/mainline/ubuntu jammy InRelease» не поддерживает архитектуру «i386»
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
Следующие пакеты устанавливались автоматически и больше не требуются:
  libflashrom1 libftdi1-2
Для их удаления используйте «sudo apt autoremove».
Следующие НОВЫЕ пакеты будут установлены:
  nginx
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 44 пакетов не обновлено.
Необходимо скачать 1 011 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 3 281 kB.
Пол:1 http://nginx.org/packages/mainline/ubuntu jammy/nginx amd64 nginx amd64 1.23.3-1~jammy [1 011 kB]
Получено 1 011 kB за 1с (1 668 kB/s)
Выбор ранее не выбранного пакета nginx.
(Чтение базы данных … на данный момент установлено 187455 файлов и каталогов.)
Подготовка к распаковке …/nginx_1.23.3-1~jammy_amd64.deb …
----------------------------------------------------------------------

Thanks for using nginx!

Please find the official documentation for nginx here:
* https://nginx.org/en/docs/

Please subscribe to nginx-announce mailing list to get
the most important news about nginx:
* https://nginx.org/en/support.html

Commercial subscriptions for nginx are available on:
* https://nginx.com/products/

----------------------------------------------------------------------
Распаковывается nginx (1.23.3-1~jammy) …
Настраивается пакет nginx (1.23.3-1~jammy) …
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /lib/systemd/system/nginx.service.
Обрабатываются триггеры для man-db (2.10.2-1) …
gb@gb-VirtualBox:~$ sudo zypper install curl ca-certificates gpg2
sudo: zypper: команда не найдена
gb@gb-VirtualBox:~$ sudo zypper install curl ca-certificates gpg2
sudo: zypper: команда не найдена
gb@gb-VirtualBox:~$ echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
    | sudo tee /etc/apt/preferences.d/99nginx
Package: *
Pin: origin nginx.org
Pin: release o=nginx
Pin-Priority: 900
```

```
Docker 
gb@gb-VirtualBox:~$ **sudo apt-get remove docker docker-engine docker.io containerd runc**
[sudo] пароль для gb: 
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
E: Невозможно найти пакет docker-engine
gb@gb-VirtualBox:~$ sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
Сущ:1 http://ru.archive.ubuntu.com/ubuntu jammy InRelease
Пол:2 http://ru.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]                                          
Пол:3 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]                                               
Пол:4 http://ru.archive.ubuntu.com/ubuntu jammy-backports InRelease [107 kB]                                            
Пол:5 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main i386 Packages [435 kB]                                     
Игн:6 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy InRelease                                             
Пол:7 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [874 kB]                                    
Пол:8 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main Translation-en [192 kB]                                    
Пол:9 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 DEP-11 Metadata [102 kB]                             
Пол:10 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 c-n-f Metadata [13,2 kB]                            
Пол:11 http://ru.archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [587 kB]                             
Пол:12 http://security.ubuntu.com/ubuntu jammy-security/main i386 Packages [252 kB]                                     
Пол:13 http://ru.archive.ubuntu.com/ubuntu jammy-updates/restricted Translation-en [90,9 kB]                            
Пол:14 http://ru.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [801 kB]                               
Ошб:15 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release                                              
  404  Not Found [IP: 185.125.190.52 443]
Пол:16 http://ru.archive.ubuntu.com/ubuntu jammy-updates/universe i386 Packages [568 kB]                                
Пол:17 http://ru.archive.ubuntu.com/ubuntu jammy-updates/universe Translation-en [143 kB]         
Пол:18 http://ru.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 DEP-11 Metadata [265 kB]            
Пол:19 http://ru.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 c-n-f Metadata [15,1 kB]                 
Пол:20 http://ru.archive.ubuntu.com/ubuntu jammy-updates/multiverse i386 Packages [3 180 B]           
Пол:21 http://ru.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 Packages [9 368 B]      
Пол:22 http://ru.archive.ubuntu.com/ubuntu jammy-updates/multiverse Translation-en [3 168 B]      
Пол:23 http://ru.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 DEP-11 Metadata [940 B]       
Пол:24 http://ru.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 c-n-f Metadata [456 B]      
Пол:25 http://ru.archive.ubuntu.com/ubuntu jammy-backports/main amd64 DEP-11 Metadata [7 980 B]     
Пол:26 http://ru.archive.ubuntu.com/ubuntu jammy-backports/universe amd64 DEP-11 Metadata [12,5 kB]       
Пол:27 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [622 kB]                    
Пол:28 http://security.ubuntu.com/ubuntu jammy-security/main Translation-en [130 kB]
Пол:29 http://security.ubuntu.com/ubuntu jammy-security/main amd64 DEP-11 Metadata [41,4 kB]
Пол:30 http://security.ubuntu.com/ubuntu jammy-security/main amd64 c-n-f Metadata [8 104 B]
Пол:31 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [550 kB]
Пол:32 http://security.ubuntu.com/ubuntu jammy-security/restricted Translation-en [84,7 kB]
Пол:33 http://security.ubuntu.com/ubuntu jammy-security/universe i386 Packages [490 kB]
Пол:34 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [639 kB]
Пол:35 http://security.ubuntu.com/ubuntu jammy-security/universe Translation-en [87,9 kB]
Пол:36 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 DEP-11 Metadata [13,3 kB]
Пол:37 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 c-n-f Metadata [11,3 kB]
Чтение списков пакетов… Готово                                                                                          
E: Репозиторий «https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release» не содержит файла Release.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
Уже установлен пакет lsb-release самой новой версии (11.1.0ubuntu4).
Уже установлен пакет ca-certificates самой новой версии (20211016ubuntu0.22.04.1).
Уже установлен пакет curl самой новой версии (7.81.0-1ubuntu1.7).
Уже установлен пакет gnupg самой новой версии (2.2.27-3ubuntu2.1).
Следующие пакеты устанавливались автоматически и больше не требуются:
  libflashrom1 libftdi1-2
Для их удаления используйте «sudo apt autoremove».
Обновлено 0 пакетов, установлено 0 новых пакетов, для удаления отмечено 0 пакетов, и 44 пакетов не обновлено.
gb@gb-VirtualBox:~$ **sudo mkdir -m 0755 -p /etc/apt/keyrings**
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
gb@gb-VirtualBox:~$ **sudo mkdir -m 0755 -p /etc/apt/keyrings**
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
Файл '/etc/apt/keyrings/docker.gpg' существует. Записать поверх? (y/N) y
gb@gb-VirtualBox:~$ **echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null**
gb@gb-VirtualBox:~$ **sudo apt-get update**
Пол:1 https://download.docker.com/linux/ubuntu jammy InRelease [48,9 kB]
Сущ:2 http://security.ubuntu.com/ubuntu jammy-security InRelease                                                        
Игн:3 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy InRelease                                             
Сущ:4 http://ru.archive.ubuntu.com/ubuntu jammy InRelease                                                   
Сущ:5 http://ru.archive.ubuntu.com/ubuntu jammy-updates InRelease                                           
Сущ:6 http://ru.archive.ubuntu.com/ubuntu jammy-backports InRelease                                         
Пол:7 https://download.docker.com/linux/ubuntu jammy/stable amd64 Packages [12,7 kB]                        
Ошб:8 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release                                   
  404  Not Found [IP: 185.125.190.52 443]
Чтение списков пакетов… Готово            
E: Репозиторий «https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release» не содержит файла Release.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).
gb@gb-VirtualBox:~$ **sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin**
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово         
Следующие пакеты устанавливались автоматически и больше не требуются:
  libflashrom1 libftdi1-2
Для их удаления используйте «sudo apt autoremove».
Будут установлены следующие дополнительные пакеты:
  docker-ce-rootless-extras docker-scan-plugin git git-man liberror-perl libslirp0 pigz slirp4netns
Предлагаемые пакеты:
  aufs-tools cgroupfs-mount | cgroup-lite git-daemon-run | git-daemon-sysvinit git-doc git-email git-gui gitk gitweb
  git-cvs git-mediawiki git-svn
Следующие НОВЫЕ пакеты будут установлены:
  containerd.io docker-buildx-plugin docker-ce docker-ce-cli docker-ce-rootless-extras docker-compose-plugin
  docker-scan-plugin git git-man liberror-perl libslirp0 pigz slirp4netns
Обновлено 0 пакетов, установлено 13 новых пакетов, для удаления отмечено 0 пакетов, и 44 пакетов не обновлено.
Необходимо скачать 115 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 417 MB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu jammy/universe amd64 pigz amd64 2.6-1 [63,6 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 liberror-perl all 0.17029-1 [26,5 kB]
Пол:3 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 git-man all 1:2.34.1-1ubuntu1.6 [953 kB]
Пол:4 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 git amd64 1:2.34.1-1ubuntu1.6 [3 142 kB]
Пол:5 https://download.docker.com/linux/ubuntu jammy/stable amd64 containerd.io amd64 1.6.16-1 [27,7 MB]
Пол:6 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 libslirp0 amd64 4.6.1-1build1 [61,5 kB]
Пол:7 http://ru.archive.ubuntu.com/ubuntu jammy/universe amd64 slirp4netns amd64 1.0.1-2 [28,2 kB]
Пол:8 https://download.docker.com/linux/ubuntu jammy/stable amd64 docker-buildx-plugin amd64 0.10.2-1~ubuntu.22.04~jammy [25,9 MB]
Пол:9 https://download.docker.com/linux/ubuntu jammy/stable amd64 docker-ce-cli amd64 5:23.0.0-1~ubuntu.22.04~jammy [13,2 MB]
Пол:10 https://download.docker.com/linux/ubuntu jammy/stable amd64 docker-ce amd64 5:23.0.0-1~ubuntu.22.04~jammy [22,0 MB]
Пол:11 https://download.docker.com/linux/ubuntu jammy/stable amd64 docker-ce-rootless-extras amd64 5:23.0.0-1~ubuntu.22.04~jammy [8 759 kB]
Пол:12 https://download.docker.com/linux/ubuntu jammy/stable amd64 docker-compose-plugin amd64 2.15.1-1~ubuntu.22.04~jammy [9 570 kB]
Пол:13 https://download.docker.com/linux/ubuntu jammy/stable amd64 docker-scan-plugin amd64 0.23.0~ubuntu-jammy [3 623 kB]
Получено 115 MB за 23с (4 984 kB/s)                                                                                     
Выбор ранее не выбранного пакета pigz.
(Чтение базы данных … на данный момент установлено 186202 файла и каталога.)
Подготовка к распаковке …/00-pigz_2.6-1_amd64.deb …
Распаковывается pigz (2.6-1) …
Выбор ранее не выбранного пакета containerd.io.
Подготовка к распаковке …/01-containerd.io_1.6.16-1_amd64.deb …
Распаковывается containerd.io (1.6.16-1) …
Выбор ранее не выбранного пакета docker-buildx-plugin.
Подготовка к распаковке …/02-docker-buildx-plugin_0.10.2-1~ubuntu.22.04~jammy_amd64.deb …
Распаковывается docker-buildx-plugin (0.10.2-1~ubuntu.22.04~jammy) …
Выбор ранее не выбранного пакета docker-ce-cli.
Подготовка к распаковке …/03-docker-ce-cli_5%3a23.0.0-1~ubuntu.22.04~jammy_amd64.deb …
Распаковывается docker-ce-cli (5:23.0.0-1~ubuntu.22.04~jammy) …
Выбор ранее не выбранного пакета docker-ce.
Подготовка к распаковке …/04-docker-ce_5%3a23.0.0-1~ubuntu.22.04~jammy_amd64.deb …
Распаковывается docker-ce (5:23.0.0-1~ubuntu.22.04~jammy) …
Выбор ранее не выбранного пакета docker-ce-rootless-extras.
Подготовка к распаковке …/05-docker-ce-rootless-extras_5%3a23.0.0-1~ubuntu.22.04~jammy_amd64.deb …
Распаковывается docker-ce-rootless-extras (5:23.0.0-1~ubuntu.22.04~jammy) …
Выбор ранее не выбранного пакета docker-compose-plugin.
Подготовка к распаковке …/06-docker-compose-plugin_2.15.1-1~ubuntu.22.04~jammy_amd64.deb …
Распаковывается docker-compose-plugin (2.15.1-1~ubuntu.22.04~jammy) …
Выбор ранее не выбранного пакета docker-scan-plugin.
Подготовка к распаковке …/07-docker-scan-plugin_0.23.0~ubuntu-jammy_amd64.deb …
Распаковывается docker-scan-plugin (0.23.0~ubuntu-jammy) …
Выбор ранее не выбранного пакета liberror-perl.
Подготовка к распаковке …/08-liberror-perl_0.17029-1_all.deb …
Распаковывается liberror-perl (0.17029-1) …
Выбор ранее не выбранного пакета git-man.
Подготовка к распаковке …/09-git-man_1%3a2.34.1-1ubuntu1.6_all.deb …
Распаковывается git-man (1:2.34.1-1ubuntu1.6) …
Выбор ранее не выбранного пакета git.
Подготовка к распаковке …/10-git_1%3a2.34.1-1ubuntu1.6_amd64.deb …
Распаковывается git (1:2.34.1-1ubuntu1.6) …
Выбор ранее не выбранного пакета libslirp0:amd64.
Подготовка к распаковке …/11-libslirp0_4.6.1-1build1_amd64.deb …
Распаковывается libslirp0:amd64 (4.6.1-1build1) …
Выбор ранее не выбранного пакета slirp4netns.
Подготовка к распаковке …/12-slirp4netns_1.0.1-2_amd64.deb …
Распаковывается slirp4netns (1.0.1-2) …
Настраивается пакет docker-scan-plugin (0.23.0~ubuntu-jammy) …
Настраивается пакет liberror-perl (0.17029-1) …
Настраивается пакет docker-buildx-plugin (0.10.2-1~ubuntu.22.04~jammy) …
Настраивается пакет containerd.io (1.6.16-1) …
Created symlink /etc/systemd/system/multi-user.target.wants/containerd.service → /lib/systemd/system/containerd.service.
Настраивается пакет docker-compose-plugin (2.15.1-1~ubuntu.22.04~jammy) …
Настраивается пакет docker-ce-cli (5:23.0.0-1~ubuntu.22.04~jammy) …
Настраивается пакет libslirp0:amd64 (4.6.1-1build1) …
Настраивается пакет pigz (2.6-1) …
Настраивается пакет git-man (1:2.34.1-1ubuntu1.6) …
Настраивается пакет docker-ce-rootless-extras (5:23.0.0-1~ubuntu.22.04~jammy) …
Настраивается пакет slirp4netns (1.0.1-2) …
Настраивается пакет docker-ce (5:23.0.0-1~ubuntu.22.04~jammy) …
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /lib/systemd/system/docker.socket.
Настраивается пакет git (1:2.34.1-1ubuntu1.6) …
Обрабатываются триггеры для man-db (2.10.2-1) …
Обрабатываются триггеры для libc-bin (2.35-0ubuntu3.1) …
gb@gb-VirtualBox:~$ **sudo docker run hello-world**
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:aa0cc8055b82dc2509bed2e19b275c8f463506616377219d9642221ab53cf9fe
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

gb@gb-VirtualBox:~$
```

2. Установить и удалить deb-пакет с помощью dpkg.

```
скачал файл скинул его на рабочий стол 
gb@gb-VirtualBox:~$ **ls -li**
итого 44
     1 drwxrwx--- 1 root vboxsf   64 янв 26 18:52  home
405833 drwx------ 4 gb   gb     4096 фев  9 15:25  snap
408018 drwxrwxr-x 2 gb   gb     4096 фев  6 14:22  test
406354 drwxrwxr-x 2 gb   gb     4096 фев  7 18:15  testHomeWork3
405895 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Видео
405892 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Документы
405889 drwxr-xr-x 2 gb   gb     4096 фев  9 15:49  Загрузки
405894 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Изображения
405893 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Музыка
405891 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Общедоступные
405888 drwxr-xr-x 2 gb   gb     4096 фев  9 15:49 'Рабочий стол'
405890 drwxr-xr-x 2 gb   gb     4096 янв 26 17:06  Шаблоны
gb@gb-VirtualBox:~$ **cd Рабочий\ стол**
gb@gb-VirtualBox:~/Рабочий стол$ **sudo dpkg -i mysql-apt-config_0.8.24-1_all.deb**
[sudo] пароль для gb: 
Выбор ранее не выбранного пакета mysql-apt-config.
(Чтение базы данных … на данный момент установлено 188683 файла и каталога.)
Подготовка к распаковке mysql-apt-config_0.8.24-1_all.deb …
Распаковывается mysql-apt-config (0.8.24-1) …
Настраивается пакет mysql-apt-config (0.8.24-1) …
Warning: apt-key should not be used in scripts (called from postinst maintainerscript of the package mysql-apt-config)
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
OK
gb@gb-VirtualBox:~/Рабочий стол$

нужно менять язык системы на английский 

удаление (поменял язык) 
gb@gb-VirtualBox:~$ **sudo dpkg -P mysql-apt-config** 
[sudo] password for gb: 
(Reading database ... 188688 files and directories currently installed.)
Removing mysql-apt-config (0.8.24-1) ...
Purging configuration files for mysql-apt-config (0.8.24-1) ...
gb@gb-VirtualBox:~$

 
```

3. Установить и удалить snap-пакет. 

```
gb@gb-VirtualBox:~$ **sudo apt install snapd**
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libflashrom1 libftdi1-2
Use 'sudo apt autoremove' to remove them.
The following packages will be upgraded:
  snapd
1 to upgrade, 0 to newly install, 0 to remove and 43 not to upgrade.
Need to get 23.8 MB of archives.
After this operation, 336 kB of additional disk space will be used.
Get:1 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 snapd amd64 2.58+22.04 [23.8 MB]
Fetched 23.8 MB in 1s (19.9 MB/s) 
(Reading database ... 188683 files and directories currently installed.)
Preparing to unpack .../snapd_2.58+22.04_amd64.deb ...
Unpacking snapd (2.58+22.04) over (2.57.5+22.04ubuntu0.1) ...
Setting up snapd (2.58+22.04) ...
Installing new version of config file /etc/apt/apt.conf.d/20snapd.conf ...
snapd.failure.service is a disabled or a static unit not running, not starting it.
snapd.snap-repair.service is a disabled or a static unit not running, not starting it.
Failed to restart snapd.mounts-pre.target: Operation refused, unit snapd.mounts-pre.target may be requested by dependency only (it is configured to refuse manual start/stop).
See system logs and 'systemctl status snapd.mounts-pre.target' for details.
Could not execute systemctl:  at /usr/bin/deb-systemd-invoke line 142.
Processing triggers for gnome-menus (3.36.0-1ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for dbus (1.12.20-2ubuntu4.1) ...
Processing triggers for mailcap (3.70+nmu1ubuntu1) ...
Processing triggers for desktop-file-utils (0.26-1ubuntu3) ...
gb@gb-VirtualBox:~$ **snap find oracle**
Name                Version              Publisher     Notes    Summary
oracle-cloud-agent  1.28.0-11366         oci.osi       classic  Oracle Cloud Agent
datagrip            2022.3.3             jetbrains✓    classic  DataGrip
osddm               4.1.3.901-snap4      vasilisc      -        Oracle SQL Developer Data Modeler
dbeaver-ce          22.3.4.202302041940  dbeaver-corp  -        Universal Database Manager and SQL Client
dayon               11.0.7               regal         -        An easy-to-use, cross-platform remote desktop assistance solution
openjdk             19.0.2+7             jgneff        -        Current JDK release and early-access builds
openjfx             19.0.2.1+1           jgneff        -        Current JavaFX release and early-access builds
dbgate              5.2.2                zputil        -        DbGate
nightmare-launcher  2.0.10               xfallseane    -        Nightmare
sqlmap              1.7.tar              khiemdoan     -        Automatic SQL injection and database takeover tool
hello-java          1.0.0-1              jgneff        -        Sample Java Swing and console applications
gb@gb-VirtualBox:~$ **sudo snap install openjdk**
Загрузить пакет "core18" (2679) с канала "stable"                                Загрузитьopenjdk 19.0.2+7 from John Neffenger (jgneff) installed
gb@gb-VirtualBox:~$ **snap connections openjdk**
Interface       Plug                    Slot                 Notes
content         -                       openjdk:jdk-18-1804  -
content         -                       openjdk:jdk-19-1804  -
content         openjdk:jfx-19-1804     -                    -
desktop         openjdk:desktop         :desktop             -
desktop-legacy  openjdk:desktop-legacy  :desktop-legacy      -
gsettings       openjdk:gsettings       :gsettings           -
home            openjdk:home            :home                -
network         openjdk:network         :network             -
network-bind    openjdk:network-bind    :network-bind        -
opengl          openjdk:opengl          :opengl              -
wayland         openjdk:wayland         :wayland             -
x11             openjdk:x11             :x11                 -
gb@gb-VirtualBox:~$ **sudo snap remove openjdk**
openjdk removed
gb@gb-VirtualBox:~$
```

4. Добавить задачу для выполнения каждые 3 минуты (создание директории, запись в файл). 

```
Last login: Thu Feb  9 17:43:13 on ttys000

The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-58-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

38 updates can be applied immediately.
17 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

Last login: Thu Feb  9 17:43:23 2023 from 10.0.2.2
gb@gb-VirtualBox:~$ **crontab -e**

  GNU nano 6.2               /tmp/crontab.lpvw8t/crontab                        
# 
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
# 
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
# 
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
# 
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
# 
# For more information see the manual pages of crontab(5) and cron(8)
# 
# m h  dom mon dow   command
**3 * * * * date > /temp/date.txt**

^G Help      ^O Write Out ^W Where Is  ^K Cut       ^T Execute   ^C Location
^X Exit      ^R Read File ^\ Replace   ^U Paste     ^J Justify   ^/ Go To Line
```

5. * Подключить PPA-репозиторий на выбор. Установить из него пакет. Удалить PPA из системы.

```
Last login: Thu Feb  9 17:43:13 on ttys000

The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-58-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

38 updates can be applied immediately.
17 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

gb@gb-VirtualBox:~$ **sudo add-apt-repository ppa:gwibber-daily/ppa**
Repository: 'deb https://ppa.launchpadcontent.net/gwibber-daily/ppa/ubuntu/ jammy main'
Description:
Daily builds of Gwibber trunk
More info: https://launchpad.net/~gwibber-daily/+archive/ubuntu/ppa
Adding repository.
Press [ENTER] to continue or Ctrl-c to cancel.
Adding deb entry to /etc/apt/sources.list.d/gwibber-daily-ubuntu-ppa-jammy.list
Adding disabled deb-src entry to /etc/apt/sources.list.d/gwibber-daily-ubuntu-ppa-jammy.list
Adding key to /etc/apt/trusted.gpg.d/gwibber-daily-ubuntu-ppa.gpg with fingerprint 06D1ED00EB802A66640696C8D0AFF96872D340A3
Hit:1 http://ru.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://ru.archive.ubuntu.com/ubuntu jammy-updates InRelease              
Hit:3 http://ru.archive.ubuntu.com/ubuntu jammy-backports InRelease            
Hit:4 https://download.docker.com/linux/ubuntu jammy InRelease                 
Get:5 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]      
Ign:6 https://ppa.launchpadcontent.net/gwibber-daily/ppa/ubuntu jammy InRelease
Hit:7 http://nginx.org/packages/mainline/ubuntu jammy InRelease                
Ign:8 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy InRelease    
Err:9 https://ppa.launchpadcontent.net/gwibber-daily/ppa/ubuntu jammy Release
  404  Not Found [IP: 185.125.190.52 443]
Err:10 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release
  404  Not Found [IP: 185.125.190.52 443]
Reading package lists... Done
N: Skipping acquisition of configured file 'nginx/binary-i386/Packages', as repository 'http://nginx.org/packages/mainline/ubuntu jammy InRelease' doesn't support architecture 'i386'
E: The repository 'https://ppa.launchpadcontent.net/gwibber-daily/ppa/ubuntu jammy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
E: The repository 'https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
gb@gb-VirtualBox:~$  **sudo add-apt-repository --remove ppa:gwibber-daily/ppa**
Repository: 'deb https://ppa.launchpadcontent.net/gwibber-daily/ppa/ubuntu/ jammy main'
Description:
Daily builds of Gwibber trunk
More info: https://launchpad.net/~gwibber-daily/+archive/ubuntu/ppa
Removing repository.
Press [ENTER] to continue or Ctrl-c to cancel.
Disabling deb entry in /etc/apt/sources.list.d/gwibber-daily-ubuntu-ppa-jammy.list
Removing disabled deb entry from /etc/apt/sources.list.d/gwibber-daily-ubuntu-ppa-jammy.list
Removing disabled deb-src entry from /etc/apt/sources.list.d/gwibber-daily-ubuntu-ppa-jammy.list
Hit:1 http://ru.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://ru.archive.ubuntu.com/ubuntu jammy-updates InRelease              
Hit:3 http://ru.archive.ubuntu.com/ubuntu jammy-backports InRelease            
Hit:4 http://nginx.org/packages/mainline/ubuntu jammy InRelease                
Get:5 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]      
Ign:6 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy InRelease    
Hit:7 https://download.docker.com/linux/ubuntu jammy InRelease                 
Err:8 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release      
  404  Not Found [IP: 185.125.190.52 443]
Reading package lists... Done                            
N: Skipping acquisition of configured file 'nginx/binary-i386/Packages', as repository 'http://nginx.org/packages/mainline/ubuntu jammy InRelease' doesn't support architecture 'i386'
E: The repository 'https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
gb@gb-VirtualBox:~$
```

6. * Создать задачу резервного копирования (tar) домашнего каталога пользователя. Реализовать с использованием пользовательских crontab-файлов.Результат:

Текст команд, которые применялись при выполнении задания. При наличи: часть конфигурационных файлов, которые решают задачу. 

```
Last login: Thu Feb  9 16:09:14 on ttys000

The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
(base) iMac-iMacSON:~ imacson$ ssh -p 9022 gb@localhost
gb@localhost's password: 
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-58-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

38 updates can be applied immediately.
17 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

Last login: Thu Feb  9 16:09:21 2023 from 10.0.2.2
gb@gb-VirtualBox:~$ sudo apt update
[sudo] password for gb: 
Hit:1 http://ru.archive.ubuntu.com/ubuntu jammy InRelease
Get:2 http://ru.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]     
Hit:3 https://download.docker.com/linux/ubuntu jammy InRelease                 
Ign:4 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy InRelease    
Get:5 http://ru.archive.ubuntu.com/ubuntu jammy-backports InRelease [107 kB]   
Get:6 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]      
Get:7 http://ru.archive.ubuntu.com/ubuntu jammy/main Translation-en_GB [483 kB]
Hit:8 http://nginx.org/packages/mainline/ubuntu jammy InRelease                
Err:9 https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release      
  404  Not Found [IP: 185.125.190.52 443]
Get:10 http://ru.archive.ubuntu.com/ubuntu jammy/restricted Translation-en_GB [5,768 B]
Get:11 http://ru.archive.ubuntu.com/ubuntu jammy/universe Translation-en_GB [838 kB]
Get:12 http://ru.archive.ubuntu.com/ubuntu jammy/multiverse Translation-en_GB [102 kB]
Get:13 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 DEP-11 Metadata [101 kB]
Get:14 http://ru.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 DEP-11 Metadata [265 kB]
Get:15 http://security.ubuntu.com/ubuntu jammy-security/main amd64 DEP-11 Metadata [41.6 kB]
Get:16 http://ru.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 DEP-11 Metadata [940 B]
Get:17 http://ru.archive.ubuntu.com/ubuntu jammy-backports/main amd64 DEP-11 Metadata [7,972 B]
Get:18 http://ru.archive.ubuntu.com/ubuntu jammy-backports/universe amd64 DEP-11 Metadata [12.5 kB]
Get:19 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 DEP-11 Metadata [13.3 kB]
Reading package lists... Done                
E: The repository 'https://ppa.launchpadcontent.net/noobslab/apps/ubuntu jammy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
N: Skipping acquisition of configured file 'nginx/binary-i386/Packages', as repository 'http://nginx.org/packages/mainline/ubuntu jammy InRelease' doesn't support architecture 'i386'
gb@gb-VirtualBox:~$ sudo apt install cron
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
cron is already the newest version (3.0pl1-137ubuntu3).
cron set to manually installed.
The following packages were automatically installed and are no longer required:
  libflashrom1 libftdi1-2
Use 'sudo apt autoremove' to remove them.
0 to upgrade, 0 to newly install, 0 to remove and 43 not to upgrade.
gb@gb-VirtualBox:~$ sudo systemctl enable cron
Synchronizing state of cron.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable cron
gb@gb-VirtualBox:~$ crontab -e
no crontab for gb - using an empty one

Select an editor.  To change later, run 'select-editor'.
  1. /bin/nano        <---- easiest
  2. /usr/bin/mcedit
  3. /usr/bin/vim.tiny
  4. /bin/ed

Choose 1-4 [1]: 1

  GNU nano 6.2               /tmp/crontab.8yW52E/crontab *                      
# Edit this file to introduce tasks to be run by cron.
# 
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
# 
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
# 
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
# 
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
# 
# For example, you can run a backup of all your user accounts
 at 5 a.m every week with:
 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
# 
# For more information see the manual pages of crontab(5) and cron(8)
# 
# m h  dom mon dow   command

^G Help      ^O Write Out ^W Where Is  ^K Cut       ^T Execute   ^C Location
^X Exit      ^R Read File ^\ Replace   ^U Paste     ^J Justify   ^/ Go To Line
```

Присылаем в формате текстового документа: задание и команды для решения (без вывода). Формат - PDF (один файл на все задания).