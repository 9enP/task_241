# Конфижим для удобства

1. Где хранятся пользвательские и системные настройки подключения?

   Пользовательские настройки: `~/.ssh/config`
   
   Системные настройки: `/etc/openssh/ssh_config`
   
3. Что за файл options?

   Файл `options` — это устаревший формат конфигурации SSH клиента, который ранее использовался вместо `~/.ssh/config`. Современные версии OpenSSH его не поддерживают.
   
5. Отредактируйте файл options так, чтобы можно было подключаться не вводя имя пользвателя и порт

   <img width="337" height="27" alt="Снимок экрана 2025-12-30 в 15 14 05" src="https://github.com/user-attachments/assets/22a4cc5a-1232-4411-94fb-afe8f0356179" />

6. Назовите подключение удобным для вас спсобом
   
   Содержимое файла config:

    ```bash
    Host myserver
        HostName ternar.io
        User student
        Port 234
    ```
7. Проверьте работоспособность
   
   <img width="527" height="164" alt="image" src="https://github.com/user-attachments/assets/99ec0040-f461-4e6e-8929-f8f82a26cca0" />
