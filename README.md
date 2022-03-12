# homework

Вызов всей таблицы

SELECT g.id, g.name, q.value, p.value, s.id, m.name, m.location FROM goods g
  Join quantity q ON q.goods_id = g.id
  Join prices p ON p.goods_id = g.id
  Join suppliers s ON s.id = g.supplier_id
  Join manufacturer m ON m.id = s.manufacturer_id
  ----------------------------------------------------
  SELECT g.id, g.name AS ТОВАР, q.value AS КОЛИЧЕСТВО, p.value AS ЦЕНА, m.name AS ПРОИЗВОДИТЕЛЬ, m.location AS СТРАНА FROM goods g
  Join quantity q ON q.goods_id = g.id
  Join prices p ON p.goods_id = g.id
  Join suppliers s ON s.id = g.supplier_id
  Join manufacturer m ON m.id = s.manufacturer_id

---------------------------------------------------------------------------------
SELECT * FROM goods
  Join quantity ON quantity.goods_id = goods.id
  Join prices ON prices.goods_id = goods.id
 
 -----------------------------------------------------------
 Вызов всей таблицы
 
 SELECT * FROM goods
  Join prices ON prices.goods_id = goods.id
  Join suppliers ON suppliers.id = goods.supplier_id
  Join manufacturer ON manufacturer.id = suppliers.manufacturer_id
 
 ------------------------------------------------------------
 SELECT goods.id, goods.name, prices.value, suppliers.id, manufacturer.name, manufacturer.location FROM goods
  Join prices ON prices.goods_id = goods.id
  Join suppliers ON suppliers.id = goods.supplier_id
  Join manufacturer ON manufacturer.id = suppliers.manufacturer_id
 -------------------------------------------------------------
 SELECT g.id, g.name, pr.value, sp.id, m.name, m.location FROM goods g
	Join prices pr ON pr.goods_id = g.id
	Join suppliers sp ON sp.id = g.supplier_id
	Join manufacturer m ON m.id = sp.manufacturer_id
  --------------------------------------------------------------
 -- Найти все товары производителей из Москвы. Вывести имена товаров, их цены и имена производителей

SELECT g.id, g.name, pr.value, m.name, m.location FROM goods g
	Join prices pr ON pr.goods_id = g.id
	Join suppliers sp ON sp.id = g.supplier_id
	Join manufacturer m ON m.id = sp.manufacturer_id
WHERE m.location = 'Moscow'
------------------------------------------------------------
--Найти все товары производителей из Москвы. Вывести имена товаров, их цены и имена производителей

SELECT g.name, p.value, m.name, m.location FROM goods g
  Join quantity q ON q.goods_id = g.id
  Join prices p ON p.goods_id = g.id
  Join suppliers s ON s.id = g.supplier_id
  Join manufacturer m ON m.id = s.manufacturer_id
WHERE m.location = 'Moscow'
----------------------------------------------------------
--Найти самый дорогой товар. Вывести имя товара и его цену

SELECT g.name AS ТОВАР, p.value AS ЦЕНА FROM goods g
	Join prices p ON p.goods_id = g.id
WHERE value = (SELECT MAX(value) FROM prices)
------------------------------------------------------------
--Найти производителя с самой большой средней ценой за товары. 
--Вывести имя производителя и среднюю стоимость

SELECT m.name AS ПРОИЗВОДИТЕЛЬ, ROUND(AVG(p.value),2) FROM goods g
  Join quantity q ON q.goods_id = g.id
  Join prices p ON p.goods_id = g.id
  Join suppliers s ON s.id = g.supplier_id
  Join manufacturer m ON m.id = s.manufacturer_id
GROUP BY m.name
ORDER BY ROUND(AVG(p.value),2)
DESC
LIMIT 1
-----------------------------------------------------------
--Найти товары с нулевым остатком. Вывести имя товара и его цену

SELECT g.name, MIN(q.value) FROM goods g
  Join quantity q ON q.goods_id = g.id
  Join prices p ON p.goods_id = g.id
  Join suppliers s ON s.id = g.supplier_id
  Join manufacturer m ON m.id = s.manufacturer_id
GROUP BY g.name
ORDER BY MIN(q.value)
ASC
LIMIT 1
