# Настриваем

## 1. Какой по умолчанию используется порт для поключения?

22

## 2. Можно ли его изменить? если да то как?

Да, можно изменить порт в `/etc/openssh/sshd_config`

Раскомментировать Port 22 и поставить туда другой порт 
```bash
Port какой-то_порт
```
после изменения нужно прописать
```bash
systemctl restart sshd
```
## 3. Какая служба отвечает за обработку запросов на подключения по ssh?

Служба sshd (OpenSSH Daemon)

## 4. Какой файл конфигурации отвечает за его настройку?

/etc/ssh/sshd_config

## 5. Попробуйте подключиться по ssh к предоставленному вам серверу

<img width="827" height="189" alt="image" src="https://github.com/user-attachments/assets/0c17ea9a-560c-4476-a4ff-435348d89b00" />

## 6. Отредактируйте файл настроек на сервере так, чтобы была возможность подключиться к серверу используя пользователя root

В файле `sshd_config` изменил строку: PermitRootLogin yes

Затем проверил настройки в файле конфигурации:
<img width="662" height="103" alt="image" src="https://github.com/user-attachments/assets/13a58936-4e2a-4572-ae4a-913df05181a6" />

## 7. Измените колличество ошибок ввода пароля перед сборосом соединения, покажите эти измененения

Устанавливает максимальное количество неудачных попыток аутентификации и проверил настройку

<img width="633" height="84" alt="image" src="https://github.com/user-attachments/assets/a3ede8ef-7ed6-4f0a-b68d-54420008d60a" />

## 8. Создайте пользователя ssh-user и попробуйте им подключиться к серверу

<img width="439" height="47" alt="image" src="https://github.com/user-attachments/assets/5bb02161-d03c-4770-9eca-05e8f8177069" />

<img width="790" height="218" alt="image" src="https://github.com/user-attachments/assets/dc64a32d-0c56-47ba-a4f8-25cad602cfe4" />

## 9. Ограничте ему возможность подключения к серверу

<img width="793" height="64" alt="image" src="https://github.com/user-attachments/assets/7a9d3561-543e-439e-951d-f92016f15d56" />

<img width="452" height="59" alt="image" src="https://github.com/user-attachments/assets/d1c58111-300e-4165-a04b-53efab4c894c" />

## 10. Как вы это сделали?

Всё в тот же файл конфигурации добавил: `DenyUsers ssh-user`

## 11. Что хранится в файле known_hosts?

Файл `~/.ssh/known_hosts` содержит отпечатки ключей SSH серверов, к которым подключался пользователь. 
Это защита от атак `man-in-the-middle` - система сравнивает ключ сервера при каждом подключении с сохраненным
