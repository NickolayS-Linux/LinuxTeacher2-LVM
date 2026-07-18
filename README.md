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

Создам VG и LV. Названия: vg_root и lv_root соответственно. 

Создадим на нем файловую систему и смонтирую его, чтобы перенести туда данные:

<img width="771" height="237" alt="image" src="https://github.com/user-attachments/assets/feed3a86-4d35-4f18-baee-ec0de378920d" />

<img width="771" height="41" alt="image" src="https://github.com/user-attachments/assets/f3da4fae-2a4a-4a4d-9ec6-a3c85f14655c" />

Посмотрю, что сейчас у нас имеется:

<img width="770" height="268" alt="image" src="https://github.com/user-attachments/assets/f9bc539a-490e-4150-8de4-e403a5fb446d" />

Этой командой копируем все данные с / раздела в /mnt:

Процесс:

<img width="766" height="206" alt="image" src="https://github.com/user-attachments/assets/754ca12b-a2b5-4e75-8e34-fb15037dae5e" />

<img width="767" height="183" alt="image" src="https://github.com/user-attachments/assets/16568411-50f0-4116-8315-3b13bd1fda40" />

<img width="767" height="1002" alt="image" src="https://github.com/user-attachments/assets/a151ee14-c2f8-4e6b-a3c2-c94879e2634f" />

Процесс не быстрый, можно заварить кофи ))

ЖдемС ))

<img width="762" height="997" alt="image" src="https://github.com/user-attachments/assets/7f6b58e7-b446-4dae-b9f5-4cc065a1abe7" />

Копирование закончено:

<img width="768" height="1004" alt="image" src="https://github.com/user-attachments/assets/f168302e-ad4f-4565-965b-108b660d96f1" />

Проверим, что все скопировалось

<img width="768" height="433" alt="image" src="https://github.com/user-attachments/assets/5e8a9596-79c4-480f-af4c-7087b58cc028" />

Затем сконфигурируем grub для того, чтобы при старте перейти в новый /.

Сымитируем текущий root, сделаем в него chroot и обновим grub:

<img width="772" height="214" alt="image" src="https://github.com/user-attachments/assets/2678ad0a-5d01-49b8-9a55-e2ed6ab3e0b7" />

Обновим образ initrd

<img width="767" height="46" alt="image" src="https://github.com/user-attachments/assets/51561f00-1dd7-453e-9cfd-137e6e505dfa" />




