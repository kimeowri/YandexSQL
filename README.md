# Яндекс.Прилавок SQL
Яндекс Прилавок - это сервис, который предоставляет предпринимателям и компаниям возможность создавать собственные виртуальные магазины в онлайн-пространстве. Этот инструмент облегчает процесс создания и настройки интернет-магазинов, управления продажами и обработки заказов. Он также обеспечивает интеграцию с онлайн-платежами, что делает его полезным для развития электронной коммерции и совершения успешных онлайн-сделок.

## Содержание
- [Задачи тестировщика](#задачи-тестировщика)
- [Требования по проекту](#требования-по-проекту)
- [Инструменты](#инструменты)
- [Выполнение тестов](#выполнение-тестов)

## Задачи тестировщика
<details>
<summary> Задачи </summary> 

1. Посчитай, сколько пользователей зарегистрировано в системе. Это таблица user_model. В результате выведи только количество пользователей.
2. Добавь три новых разных продукта в таблицу product_model
3. Посчитай количество продуктов в каждой категории и вывести id только тех категорий, в которых количество продуктов больше пяти. Это таблица product_model. Результат отсортируй в порядке возрастания количества продуктов.
4. В приложение хотят добавить фичу — возможность вносить правки в заказы. Сработает только с теми заказами, где:
стоимость доставки (deliveryPrice) больше 500,
стоит статус «заказ формируется» или «заказ в доставке».
5. Выведи информацию о продуктах, цена которых находится в диапазоне от 200 до 500. Информация по каждому продукту включает: название продукта, цену, название категории, к которой он относится.
6. Для каждой карточки выведи ее название и количество продуктов (productsCount) для этой карточки. Результат отсортируй по названию карточки.
   
***

</details>

## Требования по проекту

<details>
<summary> Требования к приложению Яндекс.Прилавка </summary>

<img width="1415" alt="image" src="https://github.com/qkitech/YandexSQL/assets/157276532/e8d50f19-954d-4789-a832-1b66d7dbe3a2">

***
</details>

## Инструменты
<p align="left"> 
  <a href="https://www.postgresql.org/" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/postgresql-colored.svg" width="36" height="36" alt="PostgreSQL" /></a>
   <a href="https://iterm2.com/" target="_blank" rel="noreferrer"><img src="https://upload.wikimedia.org/wikipedia/commons/3/31/ITerm2_v3.4_icon.png" width="36" height="36" alt="ITerm2" /></a>
</p> 

## Выполнение тестов
<details>
   <summary> Решения </summary>
<details>
<summary> Задача 1 </summary>
  
```
SELECT COUNT(*) 
FROM user_model;
```

***
</details>


<details>
<summary> Задача 2 </summary>
 
```
INSERT INTO product_model (id, name, price, weight, units, "categoryId") 
VALUES (114, 'Med', 9.99, 500, 'g', 3), (115, 'Moloko', 3.49, 1000, 'ml', 2), (116, 'Yabloki' , 4.99, 1000, 'g', 1);
```

***
</details>


<details>
<summary>Задача 3</summary>

```
SELECT "categoryId" 
FROM product_model 
GROUP BY "categoryId" 
HAVING COUNT(*) > 5 
ORDER BY COUNT(*) ASC;
```

***
</details>


<details>
<summary>Задача 4 </summary>
 
```
SELECT id, 
  CASE
    WHEN "deliveryPrice" > 500 AND (status = 0 OR status = 1) THEN 'yes' ELSE 'no'  
  END update_order 
from order_model;
```

***
</details>


<details>
 <summary>Задача 5</summary>
 
```
SELECT pm.name, pm.price, cm.name 
FROM product_model AS pm 
INNER JOIN category_model AS cm ON pm."categoryId" = cm.id 
WHERE pm.price BETWEEN 200 AND 500;
```

***
</details>



<details>
<summary> Задача 6 </summary>
 
```
SELECT cm.name, SUM(km."productsCount") 
FROM card_model cm 
INNER JOIN kit_model AS km ON cm.id = km."cardId" 
GROUP BY cm.name 
ORDER BY cm.name;
```

***
</details>
</details>
