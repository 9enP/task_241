## Пишем юниты

### 1. Создайте скрипт который создаёт папку заполняет её файлами ( имена 1-4 ) и записывает в них информацию о текущей дате, версии ядра, имени компьютера и списе всех файлов в домашнем каталоге пользователя от которого выполняется скрипт( не забудьте сдлеать проверку на существование файлов и папок)

Создаем файл скрипта в домашней директории `nano ~/create_files_script.sh`

Содержимое скрипта:
```
#!/bin/bash

cd ~


FOLDER_NAME="system_info_folder"

if [ -d "$FOLDER_NAME" ]; then
    echo "Папка $FOLDER_NAME уже существует. Удаляем..."
    rm -rf "$FOLDER_NAME"
fi

mkdir "$FOLDER_NAME"
cd "$FOLDER_NAME"

echo "Создание файлов с системной информацией..."

for i in {1..4}; do
    echo "=== Файл $i ===" > file$i.txt
    echo "Дата: $(date)" >> file$i.txt
    echo "Версия ядра: $(uname -r)" >> file$i.txt
    echo "Имя компьютера: $(hostname)" >> file$i.txt
    echo "Текущий пользователь: $(whoami)" >> file$i.txt
    echo "" >> file$i.txt
    echo "Список файлов в домашней папке ($HOME):" >> file$i.txt
    echo "========================================" >> file$i.txt
    ls -la ~/ >> file$i.txt
    echo "" >> file$i.txt
    echo "Файл создан: $(date)" >> file$i.txt
    echo "Создан file$i.txt"
done

echo "Готово! Check папку: ~/$FOLDER_NAME/"
```

Даем права на выполнение `chmod +x ~/create_files_script.sh`

Проверяем права `ls -la ~/create_files_script.sh`

Запускаем скрипт для проверки `~/create_files_script.sh`

Проверяем результат `ls -la ~/system_info_folder/` , `cat ~/system_info_folder/file1.txt`

<img width="661" height="451" alt="Снимок экрана 2025-12-29 в 15 17 52" src="https://github.com/user-attachments/assets/fd54a983-de94-4d23-9691-58f7a513d46b" />

### 2. Создайте юнит который будет вызывать этот скрипт при запуске. Проверьте

Создаем файл сервиса `sudo nano /etc/systemd/system/create-files.service`

`sudo` — выполнение с правами `root`. Systemd сервисы хранятся в `/etc/systemd/system/`.

Содержимое сервиса:
```
[Unit]
Description=Create system info files service
After=network.target

[Service]
Type=oneshot
ExecStart=/home/denis/create_files_script.sh
User=denis
WorkingDirectory=/home/denis

[Install]
WantedBy=multi-user.target
```
Перезагружаем systemd для чтения нового сервиса `systemctl daemon-reload`

Проверяем синтаксис сервиса `systemctl cat create-files.service`

Запускаем сервис вручную для проверки `systemctl start create-files.service`

Проверяем статус `systemctl status create-files.service`

Включаем автозапуск при загрузке системы `systemctl enable create-files.service`

<img width="660" height="724" alt="image" src="https://github.com/user-attachments/assets/847c1873-d51e-4131-aa6b-b01b1319a817" />

### 3. Создайте таймер который будет вызывать выполнение одноимённого systemd юнита каждые 5 минут.

1. Создаем файл таймера `nano /etc/systemd/system/create-files.timer`

Содержимое таймера:
```
[Unit]
Description=Timer for create-files service
Requires=create-files.service

[Timer]
OnBootSec=5min
OnUnitActiveSec=5min
Unit=create-files.service

[Install]
WantedBy=timers.target
```
2. Перезагружаем systemd `systemctl daemon-reload`.

3. Включаем и запускаем таймер `systemctl enable create-files.timer`, `systemctl start create-files.timer`.

4. Проверяем статус таймера `systemctl status create-files.timer`.

5. Смотрим все активные таймеры `systemctl list-timers`.

6. Проверяем, запущен ли таймер `systemctl list-timers | grep create-files`.
   
<img width="656" height="563" alt="image" src="https://github.com/user-attachments/assets/94084735-1b9d-49ef-92e9-579a1d87cb93" />

### 4. От какого пользователя вызыаются юниты поумолчанию?

По умолчанию юниты выполняются от пользователя root, если не указано иное в секции [Service] с директивой User=.

### 5. Создайте пользователя от имени которого будет выполняться ваш скрипт.

1. Создаем нового пользователя `adduser scriptuser`
   
2. Проверяем, что пользователь создан `id scriptuser`

3. Смотрим домашнюю директорию пользователя `ls -la /home/scriptuser/`

4. Копируем скрипт из домашней директории denis
`cp /home/denis/create_files_script.sh /home/scriptuser/`

5. Меняем владельца на scriptuser
`chown scriptuser:scriptuser /home/scriptuser/create_files_script.sh`

6. Даем права на выполнение
`chmod +x /home/scriptuser/create_files_script.sh`

7. Проверяем
`ls -la /home/scriptuser/create_files_script.sh`

`chown scriptuser:scriptuser` — меняем владельца файла на scriptuser

`chmod` +x — даем права на выполнение

<img width="660" height="84" alt="Снимок экрана 2025-12-30 в 12 51 07" src="https://github.com/user-attachments/assets/d57b486e-31b9-4b86-a4fb-7770f41c2654" />

<img width="661" height="143" alt="Снимок экрана 2025-12-30 в 12 51 35" src="https://github.com/user-attachments/assets/892a0a90-51f7-4942-bc15-5fa7e3a46e2e" />

### 6. Дополните юнит информацией о пользователе от которого должен выплняться скрипт.

Редактим сервис
`nano /etc/systemd/system/create-files.service`

Обновленное содержимое на скрине.

<img width="659" height="404" alt="image" src="https://github.com/user-attachments/assets/5a06e668-537e-439e-bf20-bcf71f36a874" />

### 7. Дополните ваш скрипт так, что бы он независимо от местоположения всега выполнялся в домашней папке того кто его вызывает.

Скрипт уже выполняет условие пункта (тк есть `cd ~`).
