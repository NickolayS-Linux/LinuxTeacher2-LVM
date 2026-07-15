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

Расширение LVM

Допустим, перед нами встала проблема нехватки свободного места в директории /data. 

Мы можем расширить файловую систему на LV /dev/lvm_test/test за счет нового блочного устройства /dev/sdc.

Для начала так же необходимо создать PV:

<img width="797" height="51" alt="image" src="https://github.com/user-attachments/assets/6889ed55-4cdb-48ec-893d-e5fe17307525" />

Далее необходимо расширить VG добавив в него этот диск (/dev/sdc):

<img width="794" height="47" alt="image" src="https://github.com/user-attachments/assets/29667bc7-16c2-4dc7-abcb-297e1d3e7587" />

Убедимся что новый диск присутствует в новой VG:

<img width="795" height="62" alt="image" src="https://github.com/user-attachments/assets/94c7c3c0-aafa-4c92-8f22-cab5cb4ed349" />

И что места в VG прибавилось:

<img width="792" height="81" alt="image" src="https://github.com/user-attachments/assets/c36b5231-6f96-44fc-986b-8999b7f81316" />

Сымитирую занятое место с помощью команды dd для большей наглядности:

<img width="794" height="89" alt="image" src="https://github.com/user-attachments/assets/c71404e0-a0d0-46f4-93f4-42641dbfe9c5" />

Теперь у нас занято 92% дискового пространства:

<img width="798" height="58" alt="image" src="https://github.com/user-attachments/assets/66d2ebb5-4050-489f-b8b3-e2a31ace6f87" />

Увеличиваю LV за счет появившегося свободного места. Возьмем не все место — это для того, чтобы осталось место для демонстрации снапшотов:

<img width="807" height="76" alt="image" src="https://github.com/user-attachments/assets/1b6748d3-b048-4438-9c4b-b9cdfa3d475e" />

Наблюдаем, что LV расширен до 19.04Gib:

<img width="804" height="54" alt="image" src="https://github.com/user-attachments/assets/f1c75da5-2346-41e9-9689-614f2fc3b53f" />

Но файловая система при этом осталась прежнего размера:

<img width="804" height="61" alt="image" src="https://github.com/user-attachments/assets/f895ad44-a99f-44f8-b561-ca484043b1b8" />

Произведем xfs_growfs, так как я использую xfs файлову систему:

<img width="799" height="340" alt="image" src="https://github.com/user-attachments/assets/93a62b1f-5b00-4aa0-a2d7-ece5701e428d" />

Допустим я забыл оставить место на снапшоты. Можно уменьшить существующий LV с помощью команды lvreduce, 

но перед этим необходимо отмонтировать файловую систему, 

root@ubuntulinux:~# umount /data/

Проверить её на ошибки (xfs_repair, не забываем, что у нас xfs) и уменьшить ее размер: 

<img width="803" height="491" alt="image" src="https://github.com/user-attachments/assets/ecd2dcda-53fb-41a4-9b5c-13913293e56e" />









