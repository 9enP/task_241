# Открываем iptables

1. Установите iptables

   <img width="830" height="587" alt="image" src="https://github.com/user-attachments/assets/3c6fb9fa-1c6b-4ee7-be5b-061e00967b67" />

   Текущие правила iptables:

   <img width="485" height="188" alt="image" src="https://github.com/user-attachments/assets/556b0d5e-a7ad-4caf-ae48-1f1243cb676f" />

2. Проверьте осталась ли возможность подключения по ssh к вашему серверу
   
   <img width="502" height="46" alt="Снимок экрана 2025-12-30 в 17 32 57" src="https://github.com/user-attachments/assets/e885cf38-b0d9-4fd8-bc83-a849618e3efa" />

3. Почему может пропасть такая возможность?
   
   Возможность подключения по SSH может пропасть после настройки iptables,
   так как firewall начинает фильтровать входящие соединения,
   и при отсутствии правила, разрешающего TCP-порт 205, новые SSH-подключения будут заблокированы.
   
4. Откройте нужный порт на сервере чтобы восстановить подключение
   
   <img width="679" height="226" alt="Снимок экрана 2025-12-30 в 17 35 22" src="https://github.com/user-attachments/assets/14ecd990-d148-4245-994c-e2e90c740ffe" />
   
   с проверкой

5. Это будет udp или tcp прот?

   TCP, так как SSH использует TCP протокол

# Сохраняем

6. Сохраняются ли записанные вами правила после перезагрузки?

   Нет, правила iptables сбросятся после перезагрузки системы, если их не сохранить специальным образом.
   
7. Как их сохранить?

   Можно сохранить текущие правила в файл
   `sudo iptables-save | sudo tee /etc/iptables.rules > /dev/null`
   
   Для загрузки можно создать systemd-сервис:
   ```bash
   [Unit]
   Description=Restore iptables rules
   Before=network.target

   [Service]
   Type=oneshot
   ExecStart=/sbin/iptables-restore /etc/iptables.rules

   [Install]
   WantedBy=multi-user.target
   ```
