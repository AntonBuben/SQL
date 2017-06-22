# sql_ex_ru
1. Компьютерная фирма
Схема БД состоит из четырех таблиц:
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)

1
SELECT model, speed, hd
from PC 
WHERE price <500
2
SELECT DISTINCT maker
FROM Product
WHERE type='Printer'
3
SELECT model, ram, screen
FROM Laptop
WHERE price >1000
4
SELECT *
FROM Printer
WHERE color = 'y'
5
SELECT model, speed, hd
FROM PC
WHERE (cd = '12x' OR cd = '24x') 
AND price < 600
6
SELECT DISTINCT Maker, Speed
FROM Laptop
LEFT JOIN Product ON Laptop.model = Product.model
WHERE hd>=10
7
SELECT PC.model, price
FROM PC INNER JOIN   
     Product ON PC.model = Product.model
WHERE maker = 'B'
UNION
SELECT Laptop.model, price 
FROM Laptop INNER JOIN   
     Product ON Laptop.model = Product.model
WHERE maker = 'B'
UNION
SELECT Printer.model, price 
FROM Printer INNER JOIN   
     Product ON Printer.model = Product.model
WHERE maker = 'B'
8
SELECT DISTINCT maker
FROM Product 
WHERE type='PC' AND 
 maker NOT IN (SELECT DISTINCT maker 
 FROM product 
 WHERE type = 'Laptop'
 )
9
SELECT DISTINCT Product.maker
FROM PC
JOIN Product ON PC.model = Product.model
WHERE PC.speed>=450
10
SELECT model, price
FROM Printer
WHERE price >= (SELECT MAX(price) FROM Printer)
11
SELECT AVG(speed)
FROM PC
12
SELECT AVG(speed)
FROM Laptop
WHERE price > 1000
13
SELECT AVG(speed)
FROM PC INNER JOIN   
     Product ON PC.model = Product.model
WHERE maker = 'A'
14

15
SELECT hd
from PC
GROUP BY hd HAVING COUNT(hd)>=2
16

17
SELECT Product.type, Laptop.model, Laptop.speed
FROM Laptop, Product
WHERE Product.model = Laptop.model AND Laptop.speed < (SELECT MIN(PC.speed) 
 FROM PC
 )
