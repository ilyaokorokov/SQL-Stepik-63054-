### 2.1 Связи между таблицами

<details>
<summary><b>Задание №1</b></summary>
  
```mysql
CREATE TABLE author (
    author_id INT PRIMARY KEY AUTO_INCREMENT,
    name_author VARCHAR(50)
    )
```
</details>

<details>
<summary><b>Задание №2</b></summary>
  
```mysql
INSERT INTO author (name_author)
VALUES ("Булгаков М.А."), ("Достоевский Ф.М."), ("Есенин С.А."), ("Пастернак Б.Л.")
```
</details>
<details>
<summary><b>Задание №3:</b> Создание таблицы с внешними ключами.</summary>
  
```mysql
CREATE TABLE book (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(50),
    author_id INT NOT NULL,
    genre_id INT,
    price DECIMAL(8, 2),
    amount INT,
    FOREIGN KEY (author_id) REFERENCES author (author_id),
    FOREIGN KEY (genre_id) REFERENCES genre (genre_id)
    )
```
</details>
<details>
<summary><b>Задание №4:</b> Действия при удалении записи главной таблицы.</summary>
  
```mysql
CREATE TABLE book (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(50),
    author_id INT NOT NULL,
    genre_id INT,
    price DECIMAL(8, 2),
    amount INT,
    FOREIGN KEY (author_id) REFERENCES author (author_id) ON DELETE CASCADE,
    FOREIGN KEY (genre_id) REFERENCES genre (genre_id) ON DELETE SET NULL
    )
```
</details>
<details>
<summary><b>Задание №5</b></summary>
  
```mysql
INSERT INTO book (title, author_id, genre_id, price, amount)
VALUES ("Стихотворения и поэмы", 3, 2, 650.00, 15),
       ("Черный человек", 3, 2, 570.20, 6),
       ("Лирика", 4, 2, 518.99, 2)
```
</details>

### 2.2 Запросы на выборку, соединение таблиц
<details>
<summary><b>Задание №1:</b> Соединение INNER JOIN.</summary>
  
```mysql
SELECT title, name_genre, price
FROM book
INNER JOIN genre ON genre.genre_id = book.genre_id
WHERE amount > 8
ORDER BY 3 DESC
```
</details>
<details>
<summary><b>Задание №2:</b> Внешнее соединение LEFT и RIGHT OUTER JOIN.</summary>
  
```mysql
SELECT name_genre
FROM genre
LEFT JOIN book USING(genre_id)
WHERE title IS NULL
```
</details>
<details>
<summary><b>Задание №3:</b> Перекрестное соединение CROSS JOIN.</summary>
  
```mysql
SELECT name_city, name_author, DATE_ADD("2020-01-01", INTERVAL FLOOR(RAND() * 365) DAY) AS Дата
FROM city, author
ORDER BY 1, 3 DESC
```
</details>
<details>
<summary><b>Задание №4:</b> Запросы на выборку из нескольких таблиц.</summary>
  
```mysql
SELECT name_genre, title, name_author
FROM book
INNER JOIN genre ON book.genre_id = genre.genre_id
INNER JOIN author ON book.author_id = author.author_id
WHERE name_genre = "роман"
ORDER BY 2
```
</details>
<details>
<summary><b>Задание №5:</b> Запросы для нескольких таблиц с группировкой.</summary>
  
```mysql
SELECT name_author, SUM(amount) AS Количество
FROM book
RIGHT JOIN author ON book.author_id = author.author_id
GROUP BY 1
HAVING Количество < 10 OR Количество IS NULL
ORDER BY 2
```
</details>
<details>
<summary><b>Задание №6:</b> Запросы для нескольких таблиц со вложенными запросами.</summary>
  
```mysql
SELECT name_author
FROM author
LEFT JOIN book ON author.author_id = book.author_id
GROUP BY 1
HAVING COUNT(DISTINCT(genre_id)) = 1
ORDER BY 1
```
</details>
<details>
<summary><b>Задание №7:</b> Вложенные запросы в операторах соединения.</summary>
  
```mysql
SELECT title, name_author, name_genre, price, amount
FROM author
INNER JOIN book ON author.author_id = book.author_id
INNER JOIN genre ON book.genre_id = genre.genre_id
WHERE book.genre_id IN (
    SELECT genre_id
    FROM book
    GROUP BY genre_id
    HAVING SUM(amount) = (
        SELECT SUM(amount)
        FROM book
        GROUP BY genre_id
        ORDER BY 1 DESC
        LIMIT 1
        )
    )
ORDER BY 1
```
</details>
<details>
<summary><b>Задание №8:</b> Операция соединение, использование USING()</summary>
  
```mysql
SELECT book.title AS Название, name_author AS Автор, book.amount + supply.amount AS Количество
FROM author
INNER JOIN book USING(author_id)
INNER JOIN supply ON book.title = supply.title AND author.name_author = supply.author AND book.price = supply.price
```
</details>
<details>
<summary><b>Задание №9:</b> </summary>
  
```mysql
SELECT title, name_genre, price
FROM genre
INNER JOIN book USING(genre_id)
WHERE amount > 8
ORDER BY price DESC
```
</details>

### 2.3 Запросы корректировки, соединение таблиц
<details>
<summary><b>Задание №1:</b> Запросы на обновление, связанные таблицы.</summary>
  
```mysql
UPDATE book
INNER JOIN author USING(author_id)
INNER JOIN supply ON (book.title, author.name_author) = (supply.title, supply.author)
SET book.amount = book.amount + supply.amount, book.price = ((book.price * book.amount) + (supply.price * supply.amount)) / (book.amount + supply.amount), supply.amount = 0
WHERE book.price != supply.price
```
</details>
<details>
<summary><b>Задание №2:</b> Запросы на добавление, связанные таблицы.</summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №3:</b> </summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №4:</b> </summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №5:</b> </summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №6:</b> </summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №7:</b> </summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №8:</b> </summary>
  
```mysql

```
</details>

### 2.4 База данных "Интернет-магазин книг", запросы на выборку
<details>
<summary><b>Задание №1:</b> </summary>
  
```mysql

```
</details>

### 2.5 База данных "Интернет-магазин книг", запросы корректировки
<details>
<summary><b>Задание №1:</b> </summary>
  
```mysql

```
</details>
