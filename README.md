# Домашнее задание к занятию «Работа с данными (DDL/DML)» - Распутин Е.В.

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.8. Восстановите дамп в базу данных.

1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

### Решение к Заданию 1:

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

```
sudo apt update
sudo apt install mysql-server
sudo systemctl status mysql
sudo systemctl enable mysql
mysql -u root -p
```
![screen1](/img/hw-12-02-1-1.png)

![screen2](/img/hw-12-02-1-2.png)

1.2. Создайте учётную запись sys_temp.

```sql
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'YourSUPADUPApsswd666!';
```
![screen3](/img/hw-12-02-2.png)

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

```sql
SELECT user FROM mysql.user;
```
![screen4](/img/hw-12-02-3.png)

1.4. Дайте все права для пользователя sys_temp.
```sql
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
```
![screen5](/img/hw-12-02-4.png)

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

```sql
SELECT * FROM information_schema.user_privileges WHERE GRANTEE="'sys_temp'@'localhost'";
```
![screen6](/img/hw-12-02-5.png)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:
```sql
SYSTEM mysql -u sys_temp -p
SELECT user();
```
![screen7](/img/hw-12-02-6.png)

Для смены типа аутентификации с sha2 используйте запрос:
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

```bash
wget https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
```
![screen8](/img/hw-12-02-7.png)

1.8. Восстановите дамп в базу данных.
```sql
source /home/tverdyakov/sakila-db/sakila-schema.sql
source /home/tverdyakov/sakila-db/sakila-data.sql
SHOW DATABASES;
```

![screen9](/img/hw-12-02-8-01.png)

![screen10](/img/hw-12-02-8-02.png)

![screen11](/img/hw-12-02-8-03.png)

1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)
```sql
SHOW TABLES;
```
![screen12](/img/hw-12-02-9-01.png)

![screen13](/img/hw-12-02-9-02.png)

### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```bash
+---------------+--------------+
| TABLE_NAME    | COLUMN_NAME  |
+---------------+--------------+
| actor         | actor_id     |
| address       | address_id   |
| category      | category_id  |
| city          | city_id      |
| country       | country_id   |
| customer      | customer_id  |
| film          | film_id      |
| film_actor    | actor_id     |
| film_actor    | film_id      |
| film_category | film_id      |
| film_category | category_id  |
| film_text     | film_id      |
| inventory     | inventory_id |
| language      | language_id  |
| payment       | payment_id   |
| rental        | rental_id    |
| staff         | staff_id     |
| store         | store_id     |
+---------------+--------------+
```
![screen14](/img/hw-12-02-10.png)


