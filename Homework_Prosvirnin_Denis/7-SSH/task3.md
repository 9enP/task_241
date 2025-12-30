# Ключики

1. Что такое ssh ключи и зачем они нужны?

   SSH-ключи — это пара криптографических ключей, которые используются для безопасного шифрования данных и аутентификации при установлении SSH-соединений.
   
2. Как их создать?
   
   команда `ssh-keygen -t тип_ключа`
   
3. Создайт пару публичный/приватный ключ ed_25519, где они хранятся?

Приватный ключ: `~/.ssh/id_ed25519`

Публичный ключ: `~/.ssh/id_ed25519.pub`

<img width="600" height="626" alt="image" src="https://github.com/user-attachments/assets/bf7c49e1-d6b3-4d1a-9037-57a22ca28edf" />

4. Скопируйте публичный ключ на ваш сервер, в каком файле он будет храниться?

<img width="822" height="268" alt="image" src="https://github.com/user-attachments/assets/240c9d26-296d-44ef-a496-99290665a79a" />

Файл хранения публичного ключа на сервере: ~/.ssh/authorized_keys

<img width="822" height="85" alt="Снимок экрана 2025-12-30 в 15 37 54" src="https://github.com/user-attachments/assets/9551443d-2986-473f-9329-511d8b8aeb0d" />

5. Попробуйте подключиться к серверу, у вас запросили пароль?

   Пароль не потребовали
<img width="529" height="43" alt="Снимок экрана 2025-12-30 в 15 37 40" src="https://github.com/user-attachments/assets/8538f9ff-9326-49b9-8e43-6c5c51d5fbc1" />

7. Запретите подключение с паролем для всех пользователей, оставьте только с помощью ключа.
   
   В файле sshd_config заменил: #PubkeyAuthentication yes на PasswordAuthentication no

   <img width="510" height="43" alt="image" src="https://github.com/user-attachments/assets/7ba00729-7585-48cf-8da0-471986986f13" />
   
   Подключение с ключом:

   <img width="625" height="46" alt="Снимок экрана 2025-12-30 в 15 48 58" src="https://github.com/user-attachments/assets/8b707814-8394-4185-8280-2861a67808de" />

