# Домашнее задание к занятию "Система мониторинга Zabbix" - `Важничев Георгий`


### Задание 1

`Установите Zabbix Server с веб-интерфейсом.`

#### Процесс выполнения

1. `Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.`
2. `Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.`
3. `Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.`
4. `Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.`

#### Требования к результатам

1. `Прикрепите в файл README.md скриншот авторизации в админке.`
2. `Приложите в файл README.md текст использованных команд в GitHub.`

1. `Прикрепите в файл README.md скриншот авторизации в админке.`

![png](https://github.com/vajnichev/9-02-hw/blob/main/img/9.0.1.png)
![png](https://github.com/vajnichev/9-02-hw/blob/main/img/9.0.2.png)
![png](https://github.com/vajnichev/9-02-hw/blob/main/img/9.0.3.png)


2. `Приложите в файл README.md текст использованных команд в GitHub.`

```yaml
Установил PostgreSQL
sudo apt update 
sudo apt install postgresql


Установил репозиторий Zabbix
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
dpkg -i zabbix-release_latest_6.0+debian11_all.deb
apt update
 
Установил Zabbix сервер, веб-интерфейс и агент 
sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent

Создал базу данных
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix  

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix 

Настроил базу данных для Zabbix сервера

 Отредактировал файл /etc/zabbix/zabbix_server.conf
DBPassword=password DBPassword=123456789
Запустил процессы Zabbix сервера и агента
   
```

### Задание 2

 `Установите Zabbix Agent на два хоста.`

#### Процесс выполнения

1. `Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.`
2. `Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.`
3. `Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.`
4. `Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.`
5. `Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.`

#### Требования к результатам

1. `риложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу`
2. `Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером`
3. `Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.`
4. `Приложите в файл README.md текст использованных команд в GitHub`


1. `риложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу`

![png](https://github.com/vajnichev/9-02-hw/blob/main/img/9.0.4.png)


2. `Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером`

![png](https://github.com/vajnichev/9-02-hw/blob/main/img/9.0.5.png)
![png](https://github.com/vajnichev/9-02-hw/blob/main/img/9.0.6.png)


3. `Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.`

![png](https://github.com/vajnichev/9-02-hw/blob/main/img/9.0.7.png)

4. `Приложите в файл README.md текст использованных команд в GitHub`

```yaml
Установил репозиторий Zabbix
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
dpkg -i zabbix-release_latest_6.0+debian11_all.deb
apt update  

Установил Zabbix агент
sudo apt install zabbix-agent

Запустил процесс Zabbix агента
systemctl restart zabbix-agent
systemctl enable zabbix-agent   
```

