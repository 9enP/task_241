# Открываем firewald

1. Удалите iptables и установите firewalld

   Удаление:
   
   <img width="828" height="423" alt="image" src="https://github.com/user-attachments/assets/7ffd5992-6b60-4e66-8497-905bca6fb037" />

   Установка:

   <img width="832" height="524" alt="Снимок экрана 2025-12-30 в 17 50 05" src="https://github.com/user-attachments/assets/27fa201f-c13a-4b10-b675-9bd012763ce9" />

2. Попробуйте так-же проверить возможность подключения по ssh
   
   <img width="823" height="416" alt="image" src="https://github.com/user-attachments/assets/59b4bd88-f78a-454f-8ca4-549dffbe491f" />

   Проверка подключения по ssh:

   <img width="501" height="45" alt="Снимок экрана 2025-12-30 в 17 54 36" src="https://github.com/user-attachments/assets/f23585fb-ca27-42e1-8703-e0035422b8c6" />

3. Если её нет то откройте порт
   
   <img width="643" height="85" alt="Снимок экрана 2025-12-30 в 17 55 26" src="https://github.com/user-attachments/assets/6b9b0cf5-ba8b-4a75-baca-32cdcaef8855" />

4. Выведите список открытых портов с помощью firewall-cmd
   
   <img width="487" height="47" alt="Снимок экрана 2025-12-30 в 17 55 50" src="https://github.com/user-attachments/assets/03b6b060-25d8-4697-a943-b28cab6d1358" />

5. Можно ли там добавить порты по названию сервиса?

   Да, в firewalld можно добавлять порты по имени сервиса.

6. На вашей Локальной виртуальной машине попробуйте подключиться к серверу samba из предыдущих заданий
   
    <img width="476" height="45" alt="Снимок экрана 2025-12-30 в 18 03 24" src="https://github.com/user-attachments/assets/cd89c61e-e634-4e9e-a5e1-27a524012485" />

7. Если не получилось то откройте нужные порты
   
   <img width="654" height="424" alt="Снимок экрана 2025-12-30 в 18 06 24" src="https://github.com/user-attachments/assets/3d3bbc32-941f-4c74-9d5a-c49ef9c91967" />

8. Сделайте так чтобы изменения были постоянными

   В `firewalld` изменения становятся постоянными при использовании флага `--permanent`, но надо перезагрузить правила командой `firewall-cmd --reload`.


