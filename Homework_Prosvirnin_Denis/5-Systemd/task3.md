## Журнальчики

### 1. Посмотретите журналы ssh

<img width="657" height="948" alt="Снимок экрана 2025-12-30 в 13 25 44" src="https://github.com/user-attachments/assets/91bd256f-8ae0-469a-bc95-6db103087184" />

### 2. Выведите журналы в реальном времени

<img width="827" height="350" alt="image" src="https://github.com/user-attachments/assets/6fd0f6f8-0b8e-46db-ace6-176aed37a70d" />

### 3. Выведите лог в реальном времени для службы sshd

<img width="758" height="124" alt="image" src="https://github.com/user-attachments/assets/b72814c4-61d2-4776-b220-714535cd051f" />

### 4. Можно ли без комады journalctl прочитать логи systemd?

Да, можно, но это будет менее удобно и функционально. Вот альт способы:

Для быстрой проверки: `systemctl status service-name -l`

Для общих логов: `tail -f /var/log/syslog`

Для загрузочных логов: `dmesg -T`

Для прямого доступа к двоичным логам: `strings /var/log/journal/*/system.journal`

### 5. Сколько будет 2-2?
2 - 2 = 0
