# Домашнее задание к занятию «Репликация и масштабирование. Часть 1»

---

### Задание 1

На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.

*Ответить в свободной форме.*

---

### Задание 2

Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*

#### На всех:
```
wget https://dev.mysql.com/get/mysql80-community-release-el7-6.noarch.rpm
```
```
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
```
```
rpm -Uvh mysql80-community-release-el7-6.noarch.rpm
```
```
yum -y install mysql-server mysql-client
```
```
mysqld --initialize
```
```
chown -R mysql: /var/lib/mysql
```
```
mkdir -p /var/log/mysql
```
```
chown -R mysql: /var/log/mysql
```
#### Добавить в /etc/my.cnf :
```
bind-address=0.0.0.0
server-id=(1..n)
log_bin=/var/log/mysql/mybin.log
```
#### Посмотреть пароль присвоенный при инициализации бд:
```
cat /var/log/mysqld.log
```
#### Сменить пароль:
```
mysql -p
```
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY '12345';
```
```sql
FLUSH PRIVILEGES;
```
---

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

---

### Задание 3* 

Выполните конфигурацию master-master репликации. Произведите проверку.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*
