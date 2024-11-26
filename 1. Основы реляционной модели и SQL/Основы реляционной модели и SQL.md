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

```
</details>

<details>
<summary><b>Задание №8:</b> Выборка данных, логические операции.</summary>
  
  ```mysql

```
</details>

<details>
<summary><b>Задание №9:</b> Выборка данных, операторы BETWEEN, IN.</summary>
  
  ```mysql

```
</details>

<details>
<summary><b>Задание №10:</b> Выборка данных с сортировкой.</summary>
  
  ```mysql

```
</details>

<details>
<summary><b>Задание №11:</b> Выборка данных, оператор LIKE.</summary>
  
  ```mysql

```
</details>

<details>
<summary><b>Задание №12:</b> Задание.</summary>
  
  ```mysql

```
</details>

<details>
<summary><b>Задание №1:</b> Создание таблицы.</summary>
  
  ```mysql

```
</details>

<details>
<summary><b>Задание №1:</b> Создание таблицы.</summary>
  
  ```mysql

```
</details>
