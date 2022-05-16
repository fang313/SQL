# Решение задач по SQL
![image](https://user-images.githubusercontent.com/103492272/168607807-201c00fc-9656-493d-98db-20dfdbcb4bd4.png)

### Задание 1. 
Вывести имена всех когда-либо обслуживаемых пассажиров авиакомпаний  
**Решение:**  
SELECT name FROM Passenger

### Задание 2. 
Вывести названия всеx авиакомпаний  
**Решение:**  
SELECT name FROM Company

### Задание 3. 
Вывести все рейсы, совершенные из Москвы    
**Решение:**  
SELECT * FROM Trip  
WHERE town_from LIKE 'Moscow'  

### Задание 4. 
Вывести имена людей, которые заканчиваются на "man"  
**Решение:**  
SELECT name FROM Passenger  
WHERE name LIKE '%man'  

### Задание 5. 
Вывести количество рейсов, совершенных на TU-134  
**Решение:**  
SELECT COUNT(plane) AS count  
FROM Trip  
WHERE plane LIKE 'TU-134'

### Задание 6. 
Какие компании совершали перелеты на Boeing  
**Решение:**  
SELECT DISTINCT name FROM Company  
JOIN Trip  
ON Company.id=trip.company  
WHERE plane LIKE 'Boeing'  

### Задание 7. 
Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)  
**Решение:**  
SELECT DISTINCT plane  
FROM Trip  
WHERE town_to LIKE 'Moscow'  

### Задание 8. 
В какие города можно улететь из Парижа (Paris) и сколько времени это займёт  
**Решение:**  
SELECT town_to, TIMEDIFF(time_in, time_out) AS flight_time  
FROM Trip  
WHERE town_from = 'Paris'  

### Задание 9. 
Какие компании организуют перелеты с Владивостока (Vladivostok)  
**Решение:**  
SELECT DISTINCT name FROM Company  
JOIN Trip  
ON Company.id=trip.company  
WHERE town_from LIKE 'Vladivostok'  

### Задание 10. 
Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.  
**Решение:**  
SELECT * FROM Trip  
WHERE time_out  
BETWEEN '1900-01-01 10:00:00' AND '1900-01-01 14:00:00'  

### Задание 11. 
Вывести пассажиров с самым длинным именем  
**Решение:**  
SELECT name FROM Passenger  
WHERE LENGTH(name) = (SELECT MAX(LENGTH(name)) FROM Passenger)  

### Задание 12. 
Вывести id и количество пассажиров для всех прошедших полётов  
**Решение:**  
SELECT trip, COUNT(passenger) as count    
FROM Pass_in_trip  
GROUP BY trip  

### Задание 13. 
Вывести имена людей, у которых есть полный тёзка среди пассажиров  
**Решение:**  
SELECT name FROM Passenger  
GROUP BY name  
HAVING COUNT(name) > 1  

### Задание 14. 
В какие города летал Bruce Willis?  
**Решение:**  
SELECT DISTINCT town_to FROM Trip  
JOIN Pass_in_trip  
ON Trip.id=Pass_in_trip.trip  
JOIN Passenger  
ON Pass_in_trip.passenger=Passenger.id  
WHERE name = 'Bruce Willis'  

### Задание 15. 
Во сколько Стив Мартин (Steve Martin) прилетел в Лондон (London)  
**Решение:**  
SELECT time_in FROM Trip  
JOIN Pass_in_trip  
ON Trip.id=Pass_in_trip.trip  
JOIN Passenger  
ON Pass_in_trip.passenger=Passenger.id  
WHERE name='Steve Martin' AND town_to='London'  
