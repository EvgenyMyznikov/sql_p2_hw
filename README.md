# Домашнее задание к занятию «SQL. Часть 2» - Evgeny Myznikov

### Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

select concat(s.first_name,' ', s.last_name), c2.city, count(c.customer_id) 
from staff s 
join store s2 on s2.store_id = s.store_id 
join customer c on c.store_id = s2.store_id
left join address a on a.address_id = s.address_id
left join city c2 on c2.city_id = a.city_id
group by s.staff_id 
having count(c.customer_id) > 300;

### Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

select count(f.film_id) 
from film f
where f.`length` > (select avg(f2.`length`) from film f2);

### Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

select date_format(p.payment_date, "%c"), sum(p.amount), count(p.rental_id)
from payment p
where date_format(p.payment_date, "%c") = 7 
group by date_format(p.payment_date, "%c");

