# Базования настройка коммутатора
### Задание:
Часть 1. Проверка конфигурации коммутатора по умолчанию 

Часть 2. Создание сети и настройка основных параметров устройства.
* Настройте базовые параметры коммутатора
* Настройте IP-адрес для ПК

Часть 3. Проверка сетевых подключений
*	Отобразите конфигурацию устройства
*	Протестируйте сквозное соединение, отправив эхо-запрос
*	Протестируйте возможности удаленного управления с помощью Telnet.
### Топология:
![image](https://github.com/user-attachments/assets/0f02cfc6-e286-4d23-9a9f-968039db201c)

### Tabels  

Устройустро | Интерфейс | IP-адрес | Маска подсети | Шлюз по умолчанию 
--------- | -------- | ---------- | ------------- | -------------
S1 | VLAN1 | 192.168.1.2 | 255.255.255.0 |192.168.1.1
PC-A | NIC | 192.168.1.10 | 255.255.255.0 | 192.168.1.1



### Решение:
Часть 1: 
* Создаем сеть согласно топологии
* Проверяем настойки коммутатора по умолчанию

  Шаг 1:    
* Подсоедините консольный кабель, как показано в топологии. На данном этапе не подключайте кабель Ethernet компьютера PC-A.
* Примечание. При использовании Netlab отключите интерфейс F0/6 на коммутаторе S1. Это имеет такой же эффект, как отсоединение компьютера PC-A от коммутатора S1.
* Установите консольное подключение к коммутатору с компьютера PC-A с помощью Tera Term или другой программы эмуляции терминала.

Сопутствующие вопросы:  
**Почему нужно использовать консольное подключение для первоначальной настройки коммутатора?**  
_Новый кооммутатор не имеет данных и IP-адреса_  
**Почему нельзя подключиться к коммутатору через Telnet или SSH?**   
_Для подключения через Telnet и SSH необходимо назначить ip-адрес для установки соединения_
  
Шаг 2:  
* Проверяем настройки коммутатора по умолчанию
* данные IOS, свойства интерфейса, сведения о VLAN и флеш-память
* Эмуляции терминала предоставит доступ к командной строке пользовательского режима EXEC в виде Switch>
* Переходим в режим привилегироованный, командой enable, Switch#

![image](https://github.com/user-attachments/assets/edba3dbd-36f2-4028-be1b-b6b9ba4d6ec3)  

* Настроил актуальную дату и время

![image](https://github.com/user-attachments/assets/2ff0a3ef-218b-4170-aecd-af84d8181844)



* С помощью команды show version, можем посмотреть текущую версию коммутатора

![image](https://github.com/user-attachments/assets/4b3c298b-1d2f-49fb-9a03-3ad9d795f715)
![image](https://github.com/user-attachments/assets/1bc6ec7f-da75-425d-ac96-5dc7b5ea6c09)
  
* С помощью команды show running-config, смотрим текущую конфигурацию у стройства

![image](https://github.com/user-attachments/assets/2b245ae3-f25e-4750-afbd-2d696c1cada2)  
![image](https://github.com/user-attachments/assets/70ee3626-0d4f-4483-b49c-ebfed87b2e60)   

Сопутсвующие вопросы:  
**Сколько интерфейсов FastEthernet имеется на коммутаторе 2960?**  
_FastEthernet 0/1-24_  
**Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960?**  
_Gigabit Ethernet 0/1-2_  
**Каков диапазон значений, отображаемых в vty-линиях?**  
_line vty 0 4 , line vty 5 15_  
   
* Изучаем стартовую конфигурацию с помощью startup configuration.  
Появляеться сообщение startup-config is not present, так как в стартовую конфигурацию ничего не загружено

![image](https://github.com/user-attachments/assets/a8e79c64-d07c-42ea-a94f-133714cf7293)  

Изучаем характеристики VLAN1  
### Tabels  

VLAN | Name | Status | Port
-----| ----- | ---- | -----
1 | Default | Active | Fa0/1-24, G0/1-2

Все порты по дефолту находятся в первом влане 

![image](https://github.com/user-attachments/assets/cbb4dbc9-054a-4ddf-be0f-0cd55d61dcac)

Назначен ли IP-адрес сети VLAN 1?  
* нет

Какой MAC-адрес имеет SVI? 
* Вводим команду show interface VLAN 1
* Hardware is CPU Interface, address is 000c.cfb6.d27a (bia 000c.cfb6.d27a)  
* Vlan1 is administratively down, line protocol is down

![image](https://github.com/user-attachments/assets/ac3b8190-263d-4f13-af8d-551dbd79fbc2)   

Изучаем IP-свойства интерфейса SVI сети VLAN 1
* Internet address is down

![image](https://github.com/user-attachments/assets/801f06b6-739a-4f27-8b37-51a84538dd82)

Подключаем кабель Ethernet компьютера PC-A к порту 6 на коммутаторе и изучите IP-свойства интерфейса SVI сети VLAN 1
* Interface FastEthernet0/6, changed state to up

![image](https://github.com/user-attachments/assets/205be9a4-e639-4fbf-9e61-4e77ac3a3bc4)  

* Версия IOS коммутатора 15.0(2)SE4

![image](https://github.com/user-attachments/assets/c0511d3e-2948-4940-844a-b89512bfcc71)  

* System image file is "flash:c2960-lanbasek9-mz.150-2.SE4.bin"

![image](https://github.com/user-attachments/assets/5a1f477d-add3-4455-b99c-59efaee92fad)  

* FastEthernet0/6 is up, line protocol is up (connected)

![image](https://github.com/user-attachments/assets/ad0bf521-4be9-44f7-96c3-13e1e67f82a1)  

* address is 000c.cf6a.3306 (bia 000c.cf6a.3306)

* ![image](https://github.com/user-attachments/assets/2e4359ff-e6f5-4915-8bc1-ed52f1764396)

* Full-duplex, 100Mb/s

![image](https://github.com/user-attachments/assets/66eefd2b-aee5-4ad9-a7ad-ad333a5dd407)  

* 2960-lanbasek9-mz.150-2.SE4.bin

![image](https://github.com/user-attachments/assets/670a0496-997f-4f1b-9d7f-ddbff3786a66)  

Часть 2:  
 
 Шаг1:  
* Приступаем к настройке базовых параметров коммутатора
* Вводим команды
* no ip domain-lookup
* hostname S1
* service password-encryption
* enable secret class
* banner motd # Unauthorized access is strictly prohibited. #

![image](https://github.com/user-attachments/assets/d9ea0882-9590-4842-989d-6036c960744d)

Ограничиваем доступ к консольному порту
* line con 0
* password cisco
* logging synchronous

![image](https://github.com/user-attachments/assets/75c0c96a-304f-41e0-b7fb-74447f02e9d6)  

Настройте каналы виртуального соединения для удаленного управления vty  
* line vty 0 4
* password
* login local
  
![image](https://github.com/user-attachments/assets/34f5190a-209c-4bda-829f-ee3684871db0) 

Настраиваем interface VLAN1  

![image](https://github.com/user-attachments/assets/5772427e-6e8c-4a19-bd1c-6d4d562e4727)

**Для чего нужна команда login?**   
_Команда login используется для включения аутентификации при доступе к устройству через консоль, Telnet или SSH._

Шаг2:  
Настойка IP-адреса на компьтере  
* Перейдите в Панель управления
* В представлении «Категория» выбераем: Просмотр состояния сети и задач
* Вибираем: изменение параметров адаптера на левой панели
* Щелкнит правой кнопкой мыши интерфейс Ethernet и выбераем «Свойства» 
* Выбераем: Протокол Интернета версии 4 (TCP/IPv4) > Свойства
* Выбераем: Использовать следующий IP-адрес и введите IP-адрес и маску подсети  и нажмите ОК.

![image](https://github.com/user-attachments/assets/9452996e-c9f2-4226-b3d1-afcd4b6c72d2)

Часть 3:  
Проверяем сетевое подключение  
Шаг1:    
* С помощью команды show run, выводим всю текущюю конфигурацию
* Проверьте параметры VLAN 
**Какова полоса пропускания этого интерфейса?**  
_BW 100000 Kbit или 100 Мбит/с_

Шаг2:  
Проверяем скрозное соединение эхо-запросом
* C:\> ping 192.168.1.10 пинг идет
* C:\> ping 192.168.1.2 пинг идет

![image](https://github.com/user-attachments/assets/82847802-f8ea-46d3-8694-f235ac7b840c)

Шаг3:    
Проверяем удаленное управление коммутатором
* Открываем Command Promt
* Telnet 192.168.1.2
* Password : cisco
* S1>en
* Password : class
* Мы на устройстве

![image](https://github.com/user-attachments/assets/06456a7f-c59f-4a07-8a46-e8bf90cae1b0)

Вопросы для повторения  
**Зачем необходимо настраивать пароль VTY для коммутатора?**  
_Для обеспечения безопасности к удаленному доступу с устройства_
**Что нужно сделать, чтобы пароли не отправлялись в незашифрованном виде?**  
_Ввести команду service password-encryption, чтобы зашифровать пароли_


