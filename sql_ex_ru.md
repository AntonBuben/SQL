# sql_ex_ru
Компьютерная фирма
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

18---------------
SELECT p.maker, pr.price
FROM Printer pr
JOIN Product p ON pr.model=p.model
WHERE pr.price = (SELECT MIN(price) FROM Printer WHERE color = 'y')

SELECT Product.maker, MIN(Printer.price)
FROM Product
JOIN Printer ON Product.model = Printer.model
WHERE Product.type = 'Printer'
  AND Printer.color = 'y'
GROUP BY Product.maker


19
SELECT Product.maker, AVG(Laptop.screen)
FROM Product
JOIN Laptop ON Product.model =Laptop.model
WHERE Product.type = 'laptop'
GROUP BY Product.maker

20--------------
SELECT maker, COUNT(model) count
FROM Product
GROUP BY maker HAVING COUNT(model)>=3

21
SELECT Product.maker, MAX(PC.price) Price
FROM Product
JOIN PC ON Product.model = PC.model
GROUP BY Product.maker

22
SELECT Speed, AVG(Price) Price
FROM PC
GROUP BY Speed HAVING Speed >60

31
SELECT Class, Country
FROM CLasses
WHERE bore >= 16

33
SELECT ship
FROM Outcomes
WHERE battle= 'North Atlantic' AND result = 'sunk'

38
SELECT Country
FROM Classes
WHERE type='bb'
INTERSECT
SELECT Country
FROM Classes
WHERE type='bc'

40
SELECT Classes.class, Ships.name, Classes.country
FROM Classes
JOIN Ships ON Classes.class = Ships.class
WHERE Classes.numGuns >=10

42
SELECT ship, battle
FROM Outcomes
WHERE result = 'sunk'

44
SELECT name
FROM Ships
WHERE name LIKE 'R%'
UNION
SELECT ship
FROM Outcomes
WHERE ship LIKE 'R%'

45
SELECT name
FROM Ships
WHERE name LIKE '% % %'
UNION
SELECT ship
FROM Outcomes
WHERE ship LIKE '% % %'

49
SELECT Ships.name
FROM Ships
JOIN Classes ON Ships.class = Classes.class
WHERE bore >=16
