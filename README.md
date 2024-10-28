Этот Ansible проект предназначен для автоматизации установки и конфигурации сервера PostgreSQL на основе дистрибутива Debian 11.  
В рамках проекта также выполняется настройка системы логирования и архивирования данных, а также конфигурация брандмауэра для обеспечения безопасности сервера.

---
## ВАЖНО  
В playbook используется модуль ***community.postgresql.postgresql_set***, который является частью коллекции ***community.postgresql***. Возможно, эта коллекция уже установлена, если вы используете ***ansible*** пакет, но она не включена в ***ansible-core***  
  
1. ##### Чтобы проверить установлена ли коллекция:  
- `ansible-galaxy collection list | grep community.postgresql` 
  
2. ##### Для установки коллекции:  
- `ansible-galaxy collection install community.postgresql`  

---
## Перед запуском  
1. #### Изменить файл **inventory:**  
- `db_host ansible_host=[ip удалённого хоста] ansible_user=[пользователь ansible] ansible_password=[пароль пользователя ansible]`  
  
- ##### Например:  
- `db_host ansible_host=192.168.19.164 ansible_user=ansible ansible_password=ansible`  
  
2. Убедиться что пользователь ansible, на  может использовать команды sudo без пароля, проверить можно в `/etc/sudoers`
##### Должна быть примерно такая строка:  
- `ansible ALL=(ALL:ALL) NOPASSWD:ALL`  
- Где вместо ansible **ваш пользователь ansible**  

---
## Запуск  
- `ansible-playbook playbook.yml`
## ВАЖНО  
Также в плейбуке используется iptables, который блокирует все порты, кроме порта для postgres и ssh.  
В случае, если на удалённом хосте ssh работает на отличном от дефолтного порта, то нужно поменять в playbook.yml следующую строку:  
- `iptables -A INPUT -p tcp -m state --state NEW --dport 22 -j ACCEPT`  
#### На  
- `iptables -A INPUT -p tcp -m state --state NEW --dport [ваш порт] -j ACCEPT`

