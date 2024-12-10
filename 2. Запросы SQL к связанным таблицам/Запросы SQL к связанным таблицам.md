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

### 2.1 Запросы на выборку, соединение таблиц
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

```
</details>
<details>
<summary><b>Задание №1:</b> </summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №1:</b> </summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №1:</b> </summary>
  
```mysql

```
</details>
