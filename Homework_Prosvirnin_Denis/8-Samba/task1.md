# Шарим

1. Установите пакет samba
   
   <img width="811" height="344" alt="Снимок экрана 2025-12-30 в 16 02 45" src="https://github.com/user-attachments/assets/c1f9064a-7838-40de-a7da-af9cee1d9fa0" />
   
2. ЧТо такое побщая папка, зачем оно может быть нужно?
   
   Общая папка - сетевой ресурс, доступный другим компьютерам по протоколу SMB/CIFS.
   
   Нужно для:
   
   Обмена файлами в локальной сети
   
   Доступа к файлам с Windows-машин
   
   Сетевых хранилищ (NAS)
   
   Резервного копирования

3. Создайте общую папку без пароля с правами только на чтение файлов

  <img width="730" height="182" alt="Снимок экрана 2025-12-30 в 16 03 29" src="https://github.com/user-attachments/assets/ae1087ed-f99f-4811-8be7-f6858bc19f73" />

  В конец файла smb.conf добавил секцию public:

   ```bash
    [public]
       comment = Общая папка только для чтения
       path = /srv/samba/public
       browseable = yes
       read only = yes
       guest ok = yes
       create mask = 0644
       directory mask = 0755
   ```

4. Создайте общую папку с паролем с правами на чтение и запись

   <img width="564" height="205" alt="image" src="https://github.com/user-attachments/assets/cd295107-f9b2-493b-a1d4-5f73691e8299" />

   В конец файла smb.conf добавил секцию private:
   
    ```bash
    [private]
       comment = Приватная папка с записью
       path = /srv/samba/private
       browseable = yes
       read only = no
       guest ok = no
       valid users = sambauser
       create mask = 0644
       directory mask = 0755
    ```

5. Создайте общую папку с доступом для какой-то группы с полными правами

   <img width="525" height="366" alt="image" src="https://github.com/user-attachments/assets/cb2d897c-cf1e-459c-bc07-a3dc4b73bbc5" />
   
   В конец файла smb.conf добавил секцию group_shared:

      ```bash
    [group_shared]
       comment = Папка для группы
       path = /srv/samba/group_shared
       browseable = yes
       read only = no
       guest ok = no
       valid users = @sambagroup
       create mask = 0660
       directory mask = 2770
       force group = sambagroup
    ```
   
6. Создайте общую папку в которой у одной группы будет полный доступ, а у другой только доступ на чтение. Третья группа не должна иметь к ней доступа

   <img width="507" height="506" alt="Снимок экрана 2025-12-30 в 16 25 29" src="https://github.com/user-attachments/assets/e5dfd28b-dd3a-4774-8a42-aff6243007d4" />

   В конец файла smb.conf была добавлена секция multi_group:

    ```bash
    [multi_group]
       comment = Папка с разными правами для групп
       path = /srv/samba/multi_group
       browseable = yes
       read only = yes
       guest ok = no
    
       write list = @fullaccess
       read list = @fullaccess, @readonly
       invalid users = @noaccess
    
       create mask = 0660
       directory mask = 0770
    ```
