# LinuxTeacher2-LVM

Выполнение ДЗ 3 (LVM)

Создал аккаунт на GitHub - https://github.com/

Предварительно установленное и настроенное следующее ПО: 

ПК на Linux c 16 ГБ ОЗУ или виртуальная машина с системой Ubuntu.

Oracle VirtualBox (https://www.virtualbox.org/wiki/Linux_Downloads). 

Все дальнейшие действия были проверены при использовании VirtualBox 7.2.6 r172322, хостовая ОС: Ubuntu 24.04 Desktop. Гостевая система — Ubuntu 24.04.4 LTS. 

C использованием LVM и разбивкой разделов по умолчанию.

Оформить отчет в README-файле в GitHub-репозитории.

В данном руководстве рассмотрен процесс работы с LVM.

Запуск виртуальной машины с Ubuntu.

Базовый стенд

LVM - начало работы

Почти все команды требуют прав суперпользователя:

sudo -i

Для начала необходимо определиться какие устройства мы хотим использовать в 

1. Уменьшить том под / до 8G
2. 
Эту часть можно выполнить разными способами, в данном примере мы будем

уменьшать / до 8G без использования LiveCD.

Подготовлю чистый стенд.

<img width="766" height="288" alt="image" src="https://github.com/user-attachments/assets/7928c901-16b3-4a21-9fda-4c47ab46bc45" />

Подготовим временный том для / раздела:

<img width="771" height="46" alt="image" src="https://github.com/user-attachments/assets/e1f26150-ac61-4838-8b06-2dc3ecb8b57b" />

Создам VG и LV назову. Названия vg_root и lv_root соответственно

<img width="771" height="237" alt="image" src="https://github.com/user-attachments/assets/feed3a86-4d35-4f18-baee-ec0de378920d" />

