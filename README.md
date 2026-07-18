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

**Уменьшить том под / до 8G**
 
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

Проверим результат, что мы только, что сделали

<img width="771" height="301" alt="image" src="https://github.com/user-attachments/assets/ec495b1f-67a3-4973-828e-a9b2703d48a1" />

Выход из Chroot for Power Controls: я должен выйти из окружения chroot, что бы пытаетесь перезапустить виртуальную машину: 

<img width="774" height="68" alt="image" src="https://github.com/user-attachments/assets/981079c9-6167-4a0e-abe0-782f6a49e682" />

После ребута, проверим что у нас с дисками:

<img width="770" height="625" alt="image" src="https://github.com/user-attachments/assets/bb1594af-a25e-45f0-9a57-f12929871039" />

Теперь нам нужно изменить размер старой VG и вернуть на него рут. Для этого удаляем старый LV размером в 77G и создаём новый на 8G, 

создадим на нем файловую систему, подмонтируем её:

<img width="771" height="413" alt="image" src="https://github.com/user-attachments/assets/33bb356f-755c-43bd-800b-e8c01d45c1bc" />

Скопируем файлы на неё, но с исключениями, swap.img, /var/lib/pgpro/, /var/lib/docker/. Ограничение в 8гиг соотвественно нам не даст переместить:

<img width="779" height="30" alt="image" src="https://github.com/user-attachments/assets/bf45e885-ae47-4606-952c-640fb051d542" />

Процесс копирования:

<img width="760" height="993" alt="image" src="https://github.com/user-attachments/assets/ad8b38dd-ccd5-4387-be6d-d45c0c2c9be3" />

Закончили копирование:

<img width="772" height="980" alt="image" src="https://github.com/user-attachments/assets/302a7666-26ea-4a57-9d80-efd0aed7cc1d" />

Так же как в первый раз cконфигурирую grub.

<img width="772" height="655" alt="image" src="https://github.com/user-attachments/assets/c6c34ac8-f9dd-4354-9d5a-df8ef7e09068" />

Запускаю initrd

<img width="767" height="46" alt="image" src="https://github.com/user-attachments/assets/51561f00-1dd7-453e-9cfd-137e6e505dfa" />

**Выделить том под /var в зеркало**

На свободных дисках создаем зеркало /dev/sdc /dev/sdd:

<img width="780" height="56" alt="image" src="https://github.com/user-attachments/assets/e5692156-e4ef-4c38-9654-3e1e3906838f" />

Произведем некоторые действия:

<img width="778" height="391" alt="image" src="https://github.com/user-attachments/assets/91fd9a4e-72a5-4ab4-bd1d-3c8535b43444" />

По методичке нужно удалять временный lv_root, я ео удалять не буду, так как я обратно восстановлю систему после ДЗ.

**Выделить том под /home**

Выделяем том под /home по тому же принципу что делали для /var:

<img width="779" height="991" alt="image" src="https://github.com/user-attachments/assets/83292adb-1e0e-4cb5-a48b-ba86d6a25b68" />

**Работа со снапшотами**

Генерируем файлы в /home/:

<img width="777" height="423" alt="image" src="https://github.com/user-attachments/assets/a7b35635-305c-438e-8f30-abc76a2f0dc6" />

Проверим, что у нас получилось:

<img width="779" height="482" alt="image" src="https://github.com/user-attachments/assets/8c3bccdc-2147-48a6-ae96-79b54864ca01" />

Теперь удалим файлы:

<img width="779" height="482" alt="image" src="https://github.com/user-attachments/assets/8c3bccdc-2147-48a6-ae96-79b54864ca01" />

<img width="778" height="21" alt="image" src="https://github.com/user-attachments/assets/3383c84d-ff10-4c41-add8-981ad7ea2a75" />



<img width="470" height="251" alt="image" src="https://github.com/user-attachments/assets/d7e16826-dfb2-4dac-b51b-d38db3137276" />




