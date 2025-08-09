# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Лешин Роман`

### Задание 1 

Установите Zabbix Server с веб-интерфейсом.

#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

#### Требования к результатам 
1. Прикрепите в файл README.md скриншот авторизации в админке.
2. Приложите в файл README.md текст использованных команд в GitHub.

![Страница авторизации](./img/img1-1.png)
![Страница после авторизации](./img/img1-2.png)

```
git clone https://github.com/netology-code/sys-pattern-homework.git
cd sys-pattern-homework
git remote remove origin
git remote add origin https://github.com/vOrzee/9-2-zabbix_1-hw.git
git push -u origin main
git add .
git commit -m "Добавлен ответ к первому заданию"
git push
```
```
sudo apt update
sudo apt install postgresql postgresql-client postgresql-contrib
sudo -i
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
dpkg -i zabbix-release_latest_6.0+debian11_all.deb
apt update
apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo nano /etc/zabbix/zabbix_server.conf
// Далее меняем DBPassword
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```

---

### Задание 2 

Установите Zabbix Agent на два хоста.

#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

#### Требования к результатам
1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4. Приложите в файл README.md текст использованных команд в GitHub

![скриншот раздела Configuration > Hosts](./img/img2-1.png)
![скриншот лога zabbix agent первого хоста](./img/img2-2-1.png)
![скриншот лога zabbix agent второго хоста](./img/img2-2-2.png)
![скриншот раздела Monitoring > Latest data](./img/img2-3.png)

```
git add .
git commit -m "Добавлен ответ ко второму заданию"
git push
```
```
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
dpkg -i zabbix-release_latest_6.0+debian11_all.deb
apt update
apt install zabbix-agent
sudo nano /etc/zabbix/zabbix_agentd.conf
// Прописываем адрес сервера в Server=
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```
