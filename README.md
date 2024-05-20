# 12_03 Стасенко Григорий Домашнее задание к занятию «SQL. Часть 1» 12_03

## Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

![image](https://github.com/Nightnek/HW_12_03/assets/127677631/01cb0aad-5b96-430b-afd4-e80c4910f1c0)
````
SELECT DISTINCT district 
FROM address
WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
````
---
## Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.
![image](https://github.com/Nightnek/HW_12_03/assets/127677631/56f7cb18-b295-4430-9173-da5fda4d59cb)

````
SELECT payment_id, amount, CAST(payment_date AS DATE)
FROM payment
WHERE amount > 10 AND CAST(payment_date AS DATE) BETWEEN '2005-06-15' AND '2005-06-18';
````
---
## Задание 3
Получите последние пять аренд фильмов.

![image](https://github.com/Nightnek/HW_12_03/assets/127677631/25c4a16d-73f2-439a-9560-41c1c4897eea)

````
SELECT rental_id, CAST(rental_date AS DATE)
FROM rental
ORDER BY CAST(rental_date AS DATE) DESC LIMIT 5;
````
---
## Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
замените буквы 'll' в именах на 'pp'.
![image](https://github.com/Nightnek/HW_12_03/assets/127677631/c2543b3b-7b27-4bef-8a2a-182b2dcef30e)

````
SELECT customer_id, CONCAT(LOWER(REPLACE(first_name, 'LL', 'PP')), ' ', LOWER(last_name))
FROM customer
WHERE first_name LIKE 'Kelly' or first_name LIKE 'Willie';
````
---
## Задание 5*
Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.
![image](https://github.com/Nightnek/HW_12_03/assets/127677631/23574206-cf9e-44d8-8f30-a59716d6d4e4)

````
SELECT customer_id, email, SUBSTRING_INDEX(email, '@', 1), SUBSTRING_INDEX(email, '@', -1)
FROM customer;
````
---
## Задание 6*
Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

![image](https://github.com/Nightnek/HW_12_03/assets/127677631/a06d6f6f-e9d9-4de1-bcfe-96637c14e2e2)

````
SELECT customer_id, email, CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', 1), 1)), LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', 1), 2))) AS name, CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', -1), 1)), LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', -1), 2))) AS domain 
FROM customer;
````
