## Part 1. Installation of the OS

* command cat /etc/issue.

    ![alt text](../misc/images/1.PNG)

## Part 2. Creating a user

* Создание нового пользователя и добавление его в группу adm

    sudo useradd person

    sudo usermod -a -G adm person

    cat /etc/passwd

    ![alt text](../misc/images/2.PNG)

## Part 3. Setting up the OS network
* Изменение названия машины

    ![alt text](../misc/images/3_1.PNG)

* Установка временной зоны

    ![alt text](../misc/images/3_2.PNG)

* Вывод названия сетевых интерфейсов

    ![alt text](../misc/images/3_3.PNG)

    Интерфейс lo виртуальный интерфейс всегда присутствующий на linux. Используется для отладки сетевых программ и запуска серверных приложений на локальной машине. 
    У него всегда адрес 127.0.0.1

* Получаем новый IP от DHCP

    ![alt text](../misc/images/3_4.PNG)

    DHCP - Dynamic Host Configuration Protocol

* Внешний и внутренний IP

    ![alt text](../misc/images/3_5.PNG)

* Задаем статичный IP в конфигурационном файле
    sudo vim /etc/netplan/00-installer-config.yaml

    ![alt text](../misc/images/3_6.PNG)

    Применяем изменения:
    sudo netplan apply

* Перезагружаем: reboot

    Проверяем что у нас теперь статичный IP

    ![alt text](../misc/images/3_7.PNG)

    Пингуем удаленные хосты

    ![alt text](../misc/images/3_8.PNG)

    ![alt text](../misc/images/3_9.PNG)

## Part 4. OS Update
* Установка обновлений

   sudo apt upgrade

    ![alt text](../misc/images/4.PNG)

## Part 5. Using the sudo command
*  Наделение правами другого пользователя и изменение названия машина с правами root от другого пользователя:

    ![alt text](../misc/images/5.PNG)

    С помощью sudo (substitute user and do, подменить пользователя и выполнить) пользователь может выполнить привелигиированные команды без необходимости быть суперпользователем root.
## Part 6. Installing and configuring the time service
* Установка и настройка службы времени

    sudo apt install systemd-timesyncd

    sudo systemctl enable systemd-timesyncd

    sudo systemctl start systemd-timesyncd

    ![alt text](../misc/images/6.PNG)

## Part 7. Installing and using text editors
* Сохранение

    vim - :wq and Enter

    ![alt text](../misc/images/7_1.PNG)

    nano - Ctrl + O and Enter

    ![alt text](../misc/images/7_2.PNG)

    joe - Ctrl + K and X and Enter

    ![alt text](../misc/images/7_3.PNG)

* Выход без сохранения

    vim - :q!
    
    ![alt text](../misc/images/7_4.PNG)

    nano - Ctrl + X and NO

    ![alt text](../misc/images/7_5.PNG)

    joe - Ctrl + C and YES

    ![alt text](../misc/images/7_6.PNG)


* Поиск по файлу

    vim : /morrowto

    ![alt text](../misc/images/7_7.PNG)

    nano - Ctrl + W and morrowto

    ![alt text](../misc/images/7_8.PNG)

    joe - Ctrl + K and F and morrowto

    ![alt text](../misc/images/7_9.PNG)

    vim - :s/"что"/"чем"

    ![alt text](../misc/images/7_10.PNG)

    nano - Ctrl + \ 

    ![alt text](../misc/images/7_11.PNG)

    joe - Ctrl + K and F and R(eplace)
    
    ![alt text](../misc/images/7_12.PNG)

## Part 8. Installing and basic setup of the SSHD service
* sudo apt install openssh-server

* sudo systemctl enable sshd

* Изменил в файле порт с 22 на 2022
    sudo nano /etc/ssh/sshd_config

* Наличие процесса sshd

    ps -aux | grep sshd
    
    ps - команда для того чтобы посмотреть процессы
    
    -a - включает процессы других пользователей
    -u - выводит информацию в удобочитаемом формате, включая пользователя, CPU, память, время и команду
    -x - включает процессы, не привязанные к терминалу
    | - перенаправляет вывод ps -aux в команду grep
    grep sshd - команда для поиска строки "sshd"

* reboot

* netstat -tan

    ![alt text](../misc/images/8_1.PNG)
    
    Ключи:
    
    -t Отображает TCP подключения

    -a Отображает все активные TCP-подключения и порты TCP и UDP, на которых    компьютер прослушивает

    -n Отображает активные TCP-подключения, однако адреса и номера портов выражаются числовым образом и не предпринимается никаких попыток определения имен
    
* Столбцы
    Proto - протокол (tcp, udp, raw), используемый сокетом

    Recv-Q - счётчик байт не скопированных программой пользователя из этого сокета
    
    Send-Q - счётчик байтов, не подтверждённых удалённым узлом

    Local Address - адрес и номер порта локального конца сокета

    Foreign Address - адрес и номер порта удалённого конца сокета

    State - состояние сокета

    LISTEN - cокет ожидает входящих подключений

    IP-адрес 0.0.0.0 — это немаршрутизируемый адрес IPv4, который можно использовать в разных целях, в основном, в качестве адреса по умолчанию или адреса-заполнителя. Несмотря на то, что адрес 0.0.0.0 может использоваться в компьютерных сетях, он не является адресом какого-либо устройства.

## Part 9. Installing and using the top, htop utilities
* top:

    uptime 5 min

    1 user

    load average: 0.00, 0.00, 0.00

    Tasks: 130 total

    %Cpu(s): 0.0 us, 0.1 sy, 0.0 ni, 99.9 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st

    Mib Mem: 6018.2 total, 5556.9 free, 174.2 used, 287.2 buff/cache

    641

    641

* htop

    Сортировка по PID

    ![alt text](../misc/images/9_2.PNG)

    Сортировка по CPU

    ![alt text](../misc/images/9_3.PNG)

    Сортировка по MEM

    ![alt text](../misc/images/9_4.PNG)

    Сортировка по TIME

    ![alt text](../misc/images/9_5.PNG)

    Фильтр sshd

    ![alt text](../misc/images/9_6.PNG)

    Поиск syslog

    ![alt text]../misc/images/(9_7.PNG)

    Добавление hostname, clock, uptime

    ![alt text](../misc/images/9_8.PNG)

## Part 10. Using the fdisk utility
* Disk /dev/sda: 65.38 GiB, 70189383680 bytes, 137088640 sectors, 4G

    ![alt text](../misc/images/10.PNG)

    ![alt text](../misc/images/10_2.PNG)

## Part 11. Using the df utility
* df

    ![alt text](../misc/images/11.PNG)

    килобайты

* df -Th

    ![alt text](../misc/images/11_2.PNG)

    ext4

## Part 12. Using the du utility

* du

    ![alt text](../misc/images/12_1.PNG)

* du -hs /home

    ![alt text](../misc/images/12_2.PNG)

* sudo du -hs /var 

    ![alt text](../misc/images/12_3.PNG)

* sudo du -hs /var/log

    ![alt text](../misc/images/12_4.PNG)

* sudo -h /var/log/*

    ![alt text](../misc/images/12_5.PNG)

## Part 13. Installing and using the ncdu utility

* sudo apt install ncdu

* ncdu /home

    ![alt text](../misc/images/13_1.PNG)

* ncdu /var

    ![alt text](../misc/images/13_2.PNG)

* ncdu /var/log/

    ![alt text](../misc/images/13_3.PNG)

## Part 14. Working with system logs

* vim /var/log/dmesg

    vim /var/log/syslog

    vim /var/log/auth.log

* Время последнего входа: Jun 30, 02:55:35, user admin1, method login

    ![alt text](../misc/images/14_1.PNG)

* Restart sshd: sudo systemctl restart ssh

    ![alt text](../misc/images/14_2.PNG)

## Part 15. Using the CRON job scheduler

* crontab -e
*/2 * * * * uptime

* syslog, uptime is working

    ![alt text](../misc/images/15_1.PNG)
* Задачи cron
    
    ![alt text](../misc/images/15_2.PNG)

* Удалил задания из планировщика задач

    ![alt text](../misc/images/15_3.PNG)

It's all!