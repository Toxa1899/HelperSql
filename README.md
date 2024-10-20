# HelperSql

# ==================================================== INSERT - вставка данных

#добавление одной записи
# INSERT INTO person (name, last_name, age) VALUES ('John', 'Snow', '30'); 

#добавление нескольких записей
# INSERT INTO products (name, description, price) VALUES ('Телевизор LG 43 Smart', 'крутой телик', 45000), ('Микроволновка Sony MW 345', 'быстро разогревает', 15000);


# =================================  select  =========================================

# select * from person # вытащим данные 

# select name from person; # вытащим определенные данные

# select name as new_name from person; # alias(псевдоним) - псевдоним который дадим столбцу
 
# select name || ' ' ||  id from animal; # || - конкантенация

# select name, age * id from animal;
# select name, age < id from animal;

# select * from info limit 10; -первые 10

# select distinct country from info - вывести без повторения(дубликатов)
# select distinct last_name, name from animal;
# select distinct on(last_name) last_name, name,id from animal;

# =========================================== операции сравнения
# >, <, >=, <=, =, != или <>
# ======================== where - для фильтрации текста

# SELECT * FROM products WHERE name = 'Redmi K40';

# select * from person where (age > 20); # вытащим тех у кого возраст больше 20
# SELECT * FROM products WHERE price > 10000; 

# проверка на пустое значение / IS NULL / IS NOT NULL
# select * from animal where name is not null;

# Логические операции: and, or, not
# select * from animal where not age > 8;

# проверка на вхождение (in)
# select * from animal where name in ('vlad', 'John'); # IN

# like используется в предложении WHERE для поиска указанного шаблона в столбце

# select * from animal where name like 'J';

# SELECT * FROM products WHERE name = 'Redmi K40';
# SELECT * FROM products WHERE name LIKE 'Redmi K40';

# where name like 'A%' - имена нач на A
# like %@gmail.com
# %a% - что бы была а в слове
# like 'Ki_%' после только один символ
# like '__Ki%' перед 2 символа
# ilike не чувст к регистру


# SELECT * FROM products WHERE price >= 20000 AND price <= 50000;
# BETWEEN - проверка на нахождение в диапазоне
# SELECT * FROM products WHERE price BETWEEN 20000 AND 50000;


# ======================================= order by - сортирует по какомо нибуть полю

# select * from info order by last_name; # order by - сортирует по какому либо полю
# по дефолту сортировка в возраст порядке (asc), desc - наобартот (# ask/desc – возраст/убыв)
# select * from info order by id desc; 

# nulls firs/nulls last – выводит первыми нуллевые столбцы/ не нул
# select * from info order by last_name asc nulls first; # нулевые # или nulls last

# select * from info order by id desc limit 10; - в порядке убывания

# select * from info order by id desc limit 10 offset 4; - начни с 4-го 


# ==================================  # group by - группировка
# Оператор GROUP BY определяет, как строки будут группироваться.
#  group by,  having обычно исп с агрегационными функции:  sum() avg() count() min() max()

# Например, сгруппируем по типу животных, посчитав сколько у нас кошек и собак (т.е раз я групирую по типу то выйдут только 2 поля так как у нас только 2 типа животных)
# select animal, count(*) from animal group by animal;

#  посчитаем количество животных разных полов
# select count(id), gender from animal group by gender;

# Оператор HAVING указывает, какие группы будут включены в выходной результат, то есть выполняет фильтрацию групп. Его использование аналогично применению оператора WHERE.
# having тоже самое что where только исп с group by

# select count(id), gender from animal group by gender having count(id) > 7; # вывести только ту группу где количестов животных этого пола больше 7

# выведи всех животных количество которых заданного пола больше 3
# select animal, count(*), gender from animal group by animal, gender having count(*) > 3;

# select animal, count(*), gender from animal group by animal, gender having count(*) > 3 and gender = 'ж';
# или
# select animal, count(*), gender from animal where gender = 'ж' group by animal, gender having count(*) > 3;

# ===================================== case как if else

# select  name, case when price > 40 then 'no' else 'ok' end from product

# ============================================================================ ALTER TABLE редактирование таблицы

#переименование таблицы
# ALTER TABLE название_таблицы RENAME TO новое_название;

#добавление нового столбца
# ALTER TABLE название_таблицы ADD COLUMN название_столбца тип ограничения;

#удаление столбца
# ALTER TABLE название_таблицы DROP COLUMN название_столбца;

#переименование столбца
# ALTER TABLE название_таблицы RENAME COLUMN старое_название TO новое_название;

#изменение типа столбца
# ALTER TABLE название_таблицы ALTER COLUMN название_столбца TYPE новый_тип;

# ALTER TABLE название_таблицы ALTER COLUMN название_столбца SET/DROP NOT NULL;

# ALTER TABLE products ALTER COLUMN price SET DEFAULT 0; # установка default

# ALTER TABLE products ALTER COLUMN price DROP DEFAULT; # удаление default

# ALTER TABLE Customers
# ADD PRIMARY KEY (Id);

# ALTER TABLE products ADD CHECK(price > 0);
# ALTER TABLE products ADD CONSTRAINT check_price CHECK(price > 0);


# ==================================================== UPDATE - редактирование данных

# update animal set last_name = 'f'; # все поменяет, это плохо
# update animal set last_name = 'f2' where name ='vlad';

#редактирование одной записи
# UPDATE products SET price = 10000 WHERE id = 1; # без id тяжело было бы сделать это

#редактирование всех записей
# UPDATE products SET price = price - 1000;

#редактирование части записей
# UPDATE products SET price = price - 1000 WHERE price > 40000;

# UPDATE users SET address = 'Moscow' WHERE id = 2; # изменение данных в таблице, всегда лучше двигаться по id

# UPDATE products SET price = 10 WHERE price = 5; 


# ============================================================== DELETE - удаление данных

# DELETE FROM products WHERE id = 1; #удаление одной записи

# DELETE FROM products WHERE price < 20000; #удаление несколько записей

# DELETE FROM products; #удаление всех записей


################################################################ join

# Для соединения строк из двух или более таблиц на основе связанного между ними столбца используется оператор JOIN. Он используется для объединения двух таблиц или получения данных оттуда. В SQL есть 4 типа соединения, а именно:

#       Inner Join (Внутреннее соединение)
#       Right Join (Правое соединение) | righn outer join
#       Left Join (Левое соединение) |  left outer join
#       Full Join (Полное соединение) | full outer join

# inner join – true, true
# left join – true, false/true
# right join - false/ null , true
# full join null . True/ null . true

# LEFT JOIN в начале берет все данные из левой(первой таблицы), а уже потом присоединяет данные из правой(второй таблицы), похоже на INNER JOIN, но INNER JOIN берет данные согласно условию, а лефт жоин сначала из левой таблицы 
# пример:
# --INNER JOIN-- тащит по запросу данные
# SELECT first_name, count FROM customers JOIN orders ON orders.customer_id = customers.id;

# --LEFT JOIN-- отличается тем, что лефт жоин вытащит все строчки из лев таблицы, а только потом добавит остальные данные
# SELECT first_name, count FROM customers LEFT JOIN orders ON orders.customer_id = customers.id;

# --RIGHT JOIN--
# SELECT count, name FROM orders RIGHT JOIN products ON orders.product_id = products.id; - подтащили данные правой таблицы

# --FULL JOIN--
# SELECT first_name, count FROM customers LEFT JOIN orders ON orders.customer_id = customers.id; - соединяет две таблицы, сначала вытащит совпадения(данные, которые есть и в одной и в другой ), потом остальные данные



############################## 1 к 1
# references - упоминается 

# CREATE TABLE person(
#     id serial primary key,
#     name varchar(50) not null,
#     surname varchar(50),
#     age int
# )

# CREATE TABLE passport(e
    # id serial primary key,
    # pin int NOT null,
    # person_id int unique references person(id)
# );

######################################### 1 к *
# CREATE TABLE category(
#     id serial primary key,
#     name varchar(50)
# );


# CREATE TABLE Product(
    # Id SERIAL PRIMARY KEY,
    # name TEXT,
	#   CategoryId INTEGER,
    # FOREIGN KEY (CategoryId) REFERENCES Category (id) );

###################################### * к *

# create table teacher(
#     id serial primary key,
#     name text
# );

# create table student(
#     id serial primary key,
#     name text,
# );

# create table StudentTeacher(
#     id serial primary key,
#     id_teacher int  references teacher(id) on delete cascade,
#     id_student int  references student(id) on delete cascade,     
    
# );
