
1. Напишите запрос по своей базе с регулярным выражением, добавьте пояснение, что вы хотите найти.

Найти поставщиков, в наименовании которых есть МЕ и МА.

SELECT *
FROM catalogs.manufactures
WHERE name_manufactures ~* 'М[АЕ]';

![Регулярные выражения](D%3A%5CТАНЯ%5COTUS%5CДЗ+5%5CРегулярные+выражения.png)


2. Напишите запрос по своей базе с использованием LEFT JOIN и INNER JOIN, как порядок соединений в FROM влияет на результат? Почему?

--- INNER JOIN

Сначала отображаются данные из таблицы, которая стоит первая в запросе, а потом данные из второй таблицы.

SELECT * FROM catalogs.manufactures INNER JOIN catalogs.country_manufactures 
		ON  manufactures.id_country = country_manufactures.id_country;


![Внутреннее объединение]() 


SELECT * FROM catalogs.country_manufactures INNER JOIN catalogs.manufactures 
		ON  manufactures.id_country = country_manufactures.id_country;


![Внутреннее объединение2]() 


--- LEFT JOIN

Сначала выводятся данные из левой таблицы.


SELECT * FROM catalogs.manufactures LEFT JOIN catalogs.country_manufactures 
		using(id_country);


![Левое объединение]()       


SELECT * FROM catalogs.country_manufactures LEFT JOIN catalogs.manufactures 
		using(id_country);

![Левое объединение2]()


3. Напишите запрос на добавление данных с выводом информации о добавленных строках.

--Добавление данных в таблицу "Страна производителя"

INSERT INTO catalogs.country_manufactures
(name_country)
VALUES ('Вьетнам'),
       ('Россия'),
       ('Китай')
returning id_country, name_country;


![Добавление данных в таблицу]()


--Добавление данных в таблицу "Производители"

INSERT INTO catalogs.manufactures
(name_manufactures, address, id_country)
VALUES ('ИП Седов С.С.', 'г. Москва', 3),
       ('ООО СимаГлобал', 'г. Москва', 3),
       ('ООО Рич Фэмили', 'г. Санкт-Петербург', 1),
       ('ИП Кафтасьев А.А.', 'г. Екатеринбург', 2),
       ('ООО "Меркурий"', 'г. Оренбург', 3),
       ('ИП Топорпов А.А.', 'г. Москва', 2),
       ('ООО МАРКА', 'г. Екатеринбург', 3),
       ('ИП Пальгов Е.А.', 'г. Москва', 2)
returning id_manufactures, name_manufactures, address, id_country;


4.  Напишите запрос с обновлением данных используя UPDATE FROM.

SELECT * FROM catalogs.manufactures
WHERE name_manufactures = 'ООО СимаГлобал';

![Обновление данных]()


UPDATE catalogs.manufactures
SET address = 'г. Пенза'
WHERE name_manufactures = 'ООО СимаГлобал';

![Обновление данных2]()

![Обновление данных3]()


5. Напишите запрос для удаления данных с оператором DELETE используя join с другой таблицей с помощью using.

SELECT * FROM catalogs.manufactures CROSS JOIN catalogs.country_manufactures
WHERE manufactures.id_country = country_manufactures.id_country
	AND name_manufactures like 'ИП%';

![Удаление данных]()


DELETE FROM catalogs.manufactures	
	using catalogs.country_manufactures
WHERE manufactures.id_country = country_manufactures.id_country
AND name_manufactures like 'ИП%'
returning catalogs.manufactures.*, catalogs.country_manufactures.*;

1
4
6
8

![Удаление данных2]()

![Удаление данных3]()


6. Приведите пример использования утилиты COPY (по желанию)

COPY TO копирует содержимое таблицы в файл

SELECT * FROM catalogs.manufactures
WHERE id_country = 3;

COPY (SELECT * FROM catalogs.manufactures
       WHERE id_country = 3)
    TO 'D:/ТАНЯ/OTUS/ДЗ 5/test1.txt';

   