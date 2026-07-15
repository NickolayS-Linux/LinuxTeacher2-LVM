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

качестве Physical Volumes (далее - PV) для наших будущих Volume Groups (далее - VG). 

Для этого можно воспользоваться lsblk:

<img width="658" height="263" alt="image" src="https://github.com/user-attachments/assets/be6350af-3e3a-49d8-a26d-5e077ff7eb2c" />

На дисках: /dev/sdb, /dev/sdc, /dev/sdd, /dev/sde будем экспериментировать. 

Диски sdb, sdc будем использовать для базовых вещей и снапшотов. На дисках sdd,sde создадим lvm mirror. Также воспользуюсь утилитой lvmdiskscan:

<img width="680" height="215" alt="image" src="https://github.com/user-attachments/assets/fb8f228b-9a2f-4e58-8082-4373f0a36bbe" />

Для начала разметим диск для будущего использования LVM - создадим PV:

<img width="701" height="43" alt="image" src="https://github.com/user-attachments/assets/5078fb75-d88f-4f0b-a242-bd4ed72d2db5" />

Затем создавам первый уровень абстракции - VG:

<img width="397" height="42" alt="image" src="https://github.com/user-attachments/assets/c4a3709d-047e-4171-90b3-3f51c4997480" />

Создам Logical Volume (далее - LV):

<img width="696" height="47" alt="image" src="https://github.com/user-attachments/assets/ea2e4e4d-6a03-4cc9-a720-0cde7a9a4ae5" />

Получаю информацию о только что созданном Volume Group

<img width="701" height="284" alt="image" src="https://github.com/user-attachments/assets/f5c960c0-1eed-42a6-b51f-1e924dc0282c" />

Получаю информацию о том, какие диски входит в VG:

<img width="697" height="56" alt="image" src="https://github.com/user-attachments/assets/c86e12bf-b3c2-4498-b2ed-3c1872ea7b59" />





 









