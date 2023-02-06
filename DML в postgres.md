
1. Напишите запрос по своей базе с регулярным выражением, добавьте пояснение, что вы хотите найти.

Найти поставщиков, в наименовании которых есть МЕ и МА.

SELECT *
FROM catalogs.manufactures
WHERE name_manufactures ~* 'М[АЕ]';

![Регулярные выражения](Регулярные%20выражения.png)


2. Напишите запрос по своей базе с использованием LEFT JOIN и INNER JOIN, как порядок соединений в FROM влияет на результат? Почему?

--- INNER JOIN

Сначала отображаются данные из таблицы, которая стоит первая в запросе, а потом данные из второй таблицы.

SELECT * FROM catalogs.manufactures INNER JOIN catalogs.country_manufactures 
		ON  manufactures.id_country = country_manufactures.id_country;


![Внутреннее объединение](Объединение%20внутрен.png) 


SELECT * FROM catalogs.country_manufactures INNER JOIN catalogs.manufactures 
		ON  manufactures.id_country = country_manufactures.id_country;


![Внутреннее объединение2](Объединение%20внутрен2.png) 


--- LEFT JOIN

Сначала выводятся данные из левой таблицы.


SELECT * FROM catalogs.manufactures LEFT JOIN catalogs.country_manufactures 
		using(id_country);


![Левое объединение](Левое%20объединение.png)       


SELECT * FROM catalogs.country_manufactures LEFT JOIN catalogs.manufactures 
		using(id_country);

![Левое объединение2](Левое%20объединение2.png)


3. Напишите запрос на добавление данных с выводом информации о добавленных строках.

--Добавление данных в таблицу "Страна производителя"

INSERT INTO catalogs.country_manufactures
(name_country)
VALUES ('Вьетнам'),
       ('Россия'),
       ('Китай')
returning id_country, name_country;


![Добавление данных в таблицу](Запрос%20на%20добавление%20с%20выводом.png)


4.  Напишите запрос с обновлением данных используя UPDATE FROM.

SELECT * FROM catalogs.manufactures
WHERE name_manufactures = 'ООО СимаГлобал';

![Обновление данных](Обновление%20данных.png)


UPDATE catalogs.manufactures
SET address = 'г. Пенза'
WHERE name_manufactures = 'ООО СимаГлобал';

![Обновление данных2](Обновление%20данных2.png)

![Обновление данных3](Обновление%20данных3.png)


5. Напишите запрос для удаления данных с оператором DELETE используя join с другой таблицей с помощью using.

SELECT * FROM catalogs.manufactures CROSS JOIN catalogs.country_manufactures
WHERE manufactures.id_country = country_manufactures.id_country
	AND name_manufactures like 'ИП%';

![Удаление данных](Удаление%20данных.png)


DELETE FROM catalogs.manufactures	
	using catalogs.country_manufactures
WHERE manufactures.id_country = country_manufactures.id_country
AND name_manufactures like 'ИП%'
returning catalogs.manufactures.*, catalogs.country_manufactures.*;

1
4
6
8

![Удаление данных2](Удаление%20данных2.png)

![Удаление данных3](Удаление%20данных3.png)

