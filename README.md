# Домашнее задание к занятию «SQL. Часть 2» - Evgeny Myznikov

### Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

select distinct concat(s.first_name,' ', s.last_name), c.city , a.address , count(r.customer_id) 
from rental r
join staff s on s.staff_id = r.staff_id
left join address a on a.address_id = s.address_id
left join city c on c.city_id = a.city_id 
group by r.staff_id  
having count(r.customer_id) > 300 ;

### Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

select count(f.film_id) 
from film f
where f.`length` > (select avg(f2.`length`) from film f2);

### Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

select month(p.payment_date), sum(p.amount), count(p.rental_id)
from payment p
where month(p.payment_date) = 7 
group by month(p.payment_date);

