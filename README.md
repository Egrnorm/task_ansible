Этот Ansible проект предназначен для автоматизации установки и конфигурации сервера PostgreSQL. В рамках проекта также выполняется настройка системы логирования и архивирования данных, а также конфигурация брандмауэра для обеспечения безопасности сервера.

---
#### ВАЖНО
В playbook используется модуль ***community.postgresql.postgresql_set***, который является частью коллекции ***community.postgresql***, который не включена в ***ansible-core***
Чтобы проверить установлена ли коллекция: 
***ansible-galaxy collection list | grep community.postgresql***
Для установки коллекции:
***ansible-galaxy collection install community.postgresql***

---
#### Перед запуском
Нужно изменить файл inventory
db_host ansible_host=[ip хоста] ansible_user=[пользователь ansible] ansible_password=[пароль пользователя ansible]
***Например:***
db_host ansible_host=192.168.19.164 ansible_user=ansible ansible_password=ansible

P.s. убедиться что пользователь ansible может использовать команды sudo без пароля, проверить можно в ***/etc/sudoers***
Должна быть такая строка: ansible ALL=(ALL:ALL) NOPASSWD:ALL

---
#### Запуск
ansible-playbook playbook.yml

