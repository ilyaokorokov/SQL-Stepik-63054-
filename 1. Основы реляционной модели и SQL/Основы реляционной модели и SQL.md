### 1.1 Отношение (таблица)

<details>
<summary><b>Задание №1:</b> Создание таблицы.</summary>
  
```mysql
CREATE TABLE book (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(50),
    author VARCHAR(30),
    price DECIMAL(8, 2),
    amount INT
    )
```
</details>

<details>
<summary><b>Задание №2:</b> Вставка записи в таблицу.</summary>
  
```mysql
INSERT INTO book (title, author, price, amount)
VALUES ("Мастер и Маргарита", "Булгаков М.А.", 670.99, 3)
```
</details>

<details>
<summary><b>Задание №3:</b> Вставка нескольких записей в таблицу.</summary>
  
```mysql
INSERT INTO book (title, author, price, amount)
VALUES ("Белая гвардия", "Булгаков М.А.", 540.50, 5),
       ("Идиот", "Достоевский Ф.М.", 460.00, 10),
       ("Братья Карамазовы", "Достоевский Ф.М.", 799.01, 2);
```
</details>

### 1.2 Выборка данных

<details>
<summary><b>Задание №1:</b> Выборка всех данных из таблицы.</summary>
  
```mysql
SELECT *
FROM book
```
</details>

<details>
<summary><b>Задание №2:</b> Выборка отдельных столбцов из таблицы.</summary>
  
```mysql
SELECT author, title, price
FROM book
```
</details>

<details>
<summary><b>Задание №3:</b> Присвоение новых имен столбцам при формировании выборки.</summary>
  
```mysql
SELECT title AS Название, author AS Автор
FROM book
```
</details>

<details>
<summary><b>Задание №4:</b> Выборка данных с созданием вычисляемого столбца.</summary>
  
```mysql
SELECT title, amount, amount * 1.65 AS pack
FROM book
```
</details>

<details>
<summary><b>Задание №5:</b> Выборка данных, вычисляемые столбцы, математические функции.</summary>
  
```mysql
SELECT title, author, amount, ROUND((price*0.7), 2) as new_price
FROM book
```
</details>

<details>
<summary><b>Задание №6:</b> Выборка данных, вычисляемые столбцы, логические функции.</summary>
  
```mysql
SELECT author, title, ROUND(price * IF(author = "Булгаков М.А.", 1.1, IF(author = "Есенин С.А.", 1.05, 1)), 2) AS new_price
FROM book
```
</details>

<details>
<summary><b>Задание №7:</b> Выборка данных по условию.</summary>
  
```mysql
SELECT author, title, price
FROM book
WHERE amount < 10
```
</details>

<details>
<summary><b>Задание №8:</b> Выборка данных, логические операции.</summary>
  
```mysql
SELECT title, author, price, amount
FROM book
WHERE (price < 500 OR price > 600) AND price * amount >= 5000
```
</details>

<details>
<summary><b>Задание №9:</b> Выборка данных, операторы BETWEEN, IN.</summary>
  
```mysql
SELECT title, author
FROM book
WHERE (price BETWEEN 540.50 AND 800) AND amount IN (2,3,5,7)
```
</details>

<details>
<summary><b>Задание №10:</b> Выборка данных с сортировкой.</summary>
  
```mysql
SELECT author, title
FROM book
WHERE amount BETWEEN 2 AND 14
ORDER BY 1 DESC, 2 ASC
```
</details>

<details>
<summary><b>Задание №11:</b> Выборка данных, оператор LIKE.</summary>
  
```mysql
SELECT title, author
FROM book
WHERE title LIKE "_% _%" AND (author LIKE "% С._." OR  author LIKE "% _.С.")
ORDER BY 1 ASC
```
</details>

<details>
<summary><b>Задание №12:</b> Задание.</summary>
  
```mysql
SELECT title AS Название, author AS Автор
FROM book
WHERE (price BETWEEN 500 AND 600) AND amount IN (2, 3)
```
</details>

### 1.3 Запросы, групповые операции

<details>
<summary><b>Задание №1:</b> Выбор уникальных элементов столбца.</summary>
  
```mysql
SELECT amount
FROM book
GROUP BY amount
```
</details>

<details>
<summary><b>Задание №2:</b> Выборка данных, групповые функции SUM и COUNT.</summary>
  
```mysql
SELECT author AS Автор, COUNT(title) AS Различных_книг, SUM(amount) AS Количество_экземпляров
FROM book
GROUP BY 1
```
</details>
<details>
<summary><b>Задание №3:</b> Выборка данных, групповые функции MIN, MAX и AVG.</summary>
  
```mysql
SELECT author, MIN(price) AS Минимальная_цена, MAX(price) AS Максимальная_цена, AVG(price) AS Средняя_цена
FROM book
GROUP BY author
```
</details>
<details>
<summary><b>Задание №4:</b> Выборка данных c вычислением, групповые функции.</summary>
  
```mysql
SELECT author, SUM(price * amount) AS Стоимость, ROUND(SUM((price * amount * 0.18) / 1.18), 2) AS НДС, ROUND(SUM((price * amount) / 1.18), 2) AS Стоимость_без_НДС
FROM book
GROUP BY author
```
</details>
<details>
<summary><b>Задание №5:</b> Вычисления по таблице целиком.</summary>
  
```mysql
SELECT MIN(price) AS Минимальная_цена, MAX(price) AS Максимальная_цена, ROUND(AVG(price), 2) AS Средняя_цена
FROM book
```
</details>
<details>
<summary><b>Задание №6:</b> Выборка данных по условию, групповые функции.</summary>
  
```mysql
SELECT ROUND(AVG(price), 2) AS Средняя_цена, ROUND(SUM(price * amount), 2) AS Стоимость
FROM book
WHERE amount BETWEEN 5 AND 14
```
</details>
<details>
<summary><b>Задание №7:</b> Выборка данных по условию, групповые функции, WHERE и HAVING.</summary>
  
```mysql
SELECT author, SUM(price * amount) AS Стоимость
FROM book
WHERE title NOT IN ("Идиот", "Белая гвардия")
GROUP BY author
HAVING Стоимость > 5000
ORDER BY 2 DESC
```
</details>
<details>
<summary><b>Задание №8:</b> Задание.</summary>
  
```mysql
SELECT author, SUM(price * amount) AS Стоимость
FROM book
WHERE title <> "Идиот" AND title <> "Белая гвардия" AND author != "Булгаков М.А."
GROUP BY author
HAVING Стоимость > 1000
ORDER BY 2 DESC
```
</details>

### 1.4 Вложенные запросы

<details>
<summary><b>Задание №1:</b> Вложенный запрос, возвращающий одно значение.</summary>
  
```mysql
SELECT author, title, price
FROM book
WHERE price <= (
    SELECT AVG(price)
    FROM book
    )
ORDER BY 3 DESC
```
</details>
<details>
<summary><b>Задание №2:</b> Использование вложенного запроса в выражении.</summary>
  
```mysql
SELECT author, title, price
FROM book
WHERE ABS(price - (SELECT MIN(price) FROM book)) <= 150
ORDER BY 3 ASC
```
</details>
<details>
<summary><b>Задание №3:</b> Вложенный запрос, оператор IN.</summary>
  
```mysql
SELECT author, title, amount
FROM book
WHERE amount NOT IN (
    SELECT amount
    FROM book
    GROUP BY 1
    HAVING COUNT(*) > 1)
```
</details>
<details>
<summary><b>Задание №4:</b> Вложенный запрос, операторы ANY и ALL.</summary>
  
```mysql
SELECT author, title, price
FROM book
WHERE price < ANY (
    SELECT MIN(price)
    FROM book
    GROUP BY author
    )
```
</details>
<details>
<summary><b>Задание №5:</b> Вложенный запрос после SELECT.</summary>
  
```mysql
SELECT title, author, amount, ABS((SELECT MAX(amount) FROM book) - amount) AS Заказ
FROM book
HAVING Заказ > 0
```
</details>
<details>
<summary><b>Задание №6:</b> Задание.</summary>
  
```mysql
SELECT title, author, price, amount, ((SELECT MAX(amount) FROM book) - amount ) AS Заказ 
FROM book
WHERE price < ANY (SELECT MAX(price) FROM book)
HAVING Заказ > 5
```
</details>

### 1.5 Запросы корректировки данных
<details>
<summary><b>Задание №1:</b> Создание пустой таблицы.</summary>
  
```mysql
CREATE TABLE supply (
    supply_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(50),
    author VARCHAR(30),
    price DECIMAL(8, 2),
    amount INT
    )
```
</details>
<details>
<summary><b>Задание №2:</b> Добавление записей в таблицу.</summary>
  
```mysql
INSERT INTO supply (title, author, price, amount)
VALUES ("Лирика", "Пастернак Б.Л.", 518.99, 2),
       ("Черный человек", "Есенин С.А.", 570.20, 6),
       ("Белая гвардия", "Булгаков М.А.", 540.50, 7),
       ("Идиот", "Достоевский Ф.М.", 360.80, 3)
```
</details>
<details>
<summary><b>Задание №3:</b> Добавление записей из другой таблицы.</summary>
  
```mysql
INSERT INTO book (title, author, price, amount)
SELECT title, author, price, amount
FROM supply
WHERE author NOT IN ("Достоевский Ф.М.", "Булгаков М.А.")
```
</details>
<details>
<summary><b>Задание №4:</b> Добавление записей, вложенные запросы.</summary>
  
```mysql
INSERT INTO book (title, author, price, amount)
SELECT title, author, price, amount
FROM supply
WHERE author NOT IN (
    SELECT author
    FROM book
    )
```
</details>
<details>
<summary><b>Задание №5:</b> Запросы на обновление.</summary>
  
```mysql
UPDATE book
SET price = price * 0.9
WHERE amount BETWEEN 5 AND 10
```
</details>
<details>
<summary><b>Задание №6:</b> Запросы на обновление нескольких столбцов.</summary>
  
```mysql
UPDATE book
SET buy = IF(buy > amount, amount, buy),
    price = IF(buy = 0, price * 0.9, price)
```
</details>
<details>
<summary><b>Задание №7:</b> Запросы на обновление нескольких таблиц .</summary>
  
```mysql
UPDATE book, supply
SET book.amount = book.amount + supply.amount,
    book.price = (book.price + supply.price) / 2
WHERE book.title = supply.title AND book.author = supply.author
```
</details>
<details>
<summary><b>Задание №8:</b> Запросы на удаление.</summary>
  
```mysql
DELETE
FROM supply
WHERE author IN (
    SELECT author
    FROM book
    GROUP BY 1
    HAVING SUM(amount) > 10
    )
```
</details>
<details>
<summary><b>Задание №9:</b> Запросы на создание таблицы.</summary>
  
```mysql
CREATE TABLE ordering AS
SELECT author, title, (
    SELECT AVG(amount)
    FROM book
    ) AS amount
FROM book
WHERE amount < (
    SELECT AVG(amount)
    FROM book
    )
```
</details>
<details>
<summary><b>Задание №10:</b> Создание таблицы.</summary>
  
```mysql
CREATE TABLE new_table AS
SELECT author, title, price
FROM book
WHERE amount BETWEEN 5 AND 15 AND author LIKE "%С.А."
```
</details>

### 1.6 Таблица "Командировки". Запросы на выборку
<details>
<summary><b>Задание №1</b></summary>
  
```mysql
SELECT name, city, per_diem, date_first, date_last
FROM trip
WHERE name LIKE "%а %"
ORDER BY 5 DESC
```
</details>
<details>
<summary><b>Задание №2</b></summary>
  
```mysql
SELECT DISTINCT(name)
FROM trip
WHERE city = "Москва"
ORDER BY 1 ASC
```
</details>
<details>
<summary><b>Задание №3</b></summary>
  
```mysql
SELECT city, COUNT(city) AS Количество
FROM trip
GROUP BY city
ORDER BY 1 ASC
```
</details>
<details>
<summary><b>Задание №4</b></summary>
  
```mysql
SELECT city, COUNT(city) as Количество
FROM trip
GROUP BY city
ORDER BY Количество DESC
LIMIT 2
```
</details>
<details>
<summary><b>Задание №5</b></summary>
  
```mysql
SELECT name, city, (DATEDIFF(date_last, date_first) + 1) AS Длительность
FROM trip
WHERE city NOT IN ("Москва", "Санкт-Петербург")
ORDER BY 3 DESC, 1 DESC
```
</details>
<details>
<summary><b>Задание №6</b></summary>
  
```mysql
SELECT name, city, date_first, date_last
FROM trip
WHERE DATEDIFF(date_last, date_first) = (
    SELECT MIN(DATEDIFF(date_last, date_first))
    FROM trip
    )
```
</details>
<details>
<summary><b>Задание №7</b></summary>
  
```mysql
SELECT name, city, date_first, date_last
FROM trip
WHERE MONTH(date_first) = MONTH(date_last)
ORDER BY 2, 1
```
</details>
<details>
<summary><b>Задание №8</b></summary>
  
```mysql
SELECT MONTHNAME(date_first) AS Месяц, COUNT(*) AS Количество
FROM trip
GROUP BY 1
ORDER BY 2 DESC, 1
```
</details>
<details>
<summary><b>Задание №9</b></summary>
  
```mysql
SELECT name, city, date_first, (DATEDIFF(date_last, date_first) + 1) * per_diem AS Сумма
FROM trip
WHERE MONTH(date_first) = 2 OR MONTH(date_first) = 3
ORDER BY 1, 4 DESC
```
</details>
<details>
<summary><b>Задание №10</b></summary>
  
```mysql
SELECT name, SUM(per_diem * (DATEDIFF(date_last, date_first) + 1)) AS Сумма
FROM trip
GROUP BY 1
HAVING COUNT(*) > 3
ORDER BY 2 DESC
```
</details>

### 1.7 Таблица "Нарушения ПДД". Запросы, корректировки
<details>
<summary><b>Задание №1</b></summary>
  
```mysql
CREATE TABLE fine (
    fine_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(30),
    number_plate VARCHAR(6),
    violation VARCHAR(50),
    sum_fine DECIMAL(8, 2),
    date_violation DATE,
    date_payment DATE
    )
```
</details>
<details>
<summary><b>Задание №2</b></summary>
  
```mysql
INSERT INTO fine (name, number_plate, violation, sum_fine, date_violation, date_payment)
VALUES ('Баранов П.Е.', 'Р523ВТ', 'Превышение скорости(от 40 до 60)', Null, '2020-02-14', Null),
('Абрамова К.А.', 'О111АВ', 'Проезд на запрещающий сигнал', Null, '2020-02-23', Null),
('Яковлев Г.Р.', 'Т330ТТ', 'Проезд на запрещающий сигнал', Null, '2020-03-03', Null)
```
</details>
<details>
<summary><b>Задание №3</b></summary>
  
```mysql
UPDATE fine, traffic_violation
SET fine.sum_fine = traffic_violation.sum_fine
WHERE fine.violation = traffic_violation.violation AND fine.sum_fine IS NULL
```
</details>
<details>
<summary><b>Задание №4</b></summary>
  
```mysql
SELECT name, number_plate, violation
FROM fine
GROUP BY 1, 2, 3
HAVING COUNT(violation) >= 2
ORDER BY 1, 2, 3
```
</details>
<details>
<summary><b>Задание №5</b></summary>
  
```mysql
UPDATE fine, (
  SELECT name, number_plate, violation
  FROM fine
  GROUP BY 1, 2, 3
  HAVING COUNT(violation) >= 2
  ) AS query_in
SET fine.sum_fine = fine.sum_fine * 2
WHERE fine.name = query_in.name AND 
      fine.number_plate = query_in.number_plate AND 
      fine.violation = query_in.violation AND
      fine.date_payment IS NULL
```
</details>
<details>
<summary><b>Задание №6</b></summary>
  
```mysql
UPDATE fine f, payment p 
SET f.date_payment = p.date_payment,
    f.sum_fine = IF(DATEDIFF(f.date_payment, f.date_violation) <= 20, f.sum_fine / 2, f.sum_fine) 
WHERE f.name = p.name AND
      f.number_plate = p.number_plate AND
      f.violation = p.violation AND
      f.date_violation = p.date_violation AND
      f.date_payment IS NULL
```
</details>
<details>
<summary><b>Задание №7</b></summary>
  
```mysql
CREATE TABLE back_payment AS (
    SELECT name, number_plate, violation, sum_fine, date_violation
    FROM fine
    WHERE date_payment IS NULL
    )
```
</details>
<details>
<summary><b>Задание №8</b></summary>
  
```mysql
DELETE 
FROM fine
WHERE date_violation < '2020-02-01'
```
</details>
