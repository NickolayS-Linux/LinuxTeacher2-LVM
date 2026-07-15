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

На примере с расширением VG мы увидим, что сюда добавится еще один диск.

Детальную информацию о LV получим командой:

<img width="697" height="268" alt="image" src="https://github.com/user-attachments/assets/6b619393-89f5-4115-ba93-a71ccc1da347" />

В кратком содержании, информацию можно получить командами vgs и lvs:

<img width="800" height="130" alt="image" src="https://github.com/user-attachments/assets/72b6c108-a89d-4483-8cca-b2744f0a82dd" />

Создаю еще один LV из свободного места. На этот раз создам не экстентами, а абсолютным значением в мегабайтах:

<img width="795" height="46" alt="image" src="https://github.com/user-attachments/assets/11d3161c-bd22-4065-bdc7-d38ce7bdf4c3" />

Полуаю информацию о LVM:

<img width="794" height="78" alt="image" src="https://github.com/user-attachments/assets/5f601597-80cf-424b-a462-0bf7b7f6428d" />

Создам на LV файловую систему и смонтирую его:

<img width="795" height="168" alt="image" src="https://github.com/user-attachments/assets/3b0bd1c9-40dc-4f5a-a64e-58c1a1753e9a" />

<img width="797" height="83" alt="image" src="https://github.com/user-attachments/assets/600c9010-df60-45c1-a4fd-7e022286cea4" />








 









