# olap_queries by @user

## ❇️ Create table
Мета, очікуваний результат, результат

```SQL
```

## 🗑 Drop table

-- [DROP TABLE] Безпечне видалення таблиці в межах транзакції (BEGIN; DROP TABLE ...; COMMIT;)

## ✨ Insert queries

IDs
``

``

``

## All colums

-- [INSERT ALL] Додавання запису з заповненням усіх полів

### Mandatory only colums

-- [INSERT DEFAULT] Додавання запису з заповненням тільки обов'язкових полів

## With returning part (RETURNING, optional)

-- [INSERT RETURNING] Додавання запису з поверненням згенерованих значень (RETURNING)

## Some interesting examples (optional)

-- [INSERT ... SELECT] Вставка аналітичних даних з іншої таблиці на основі підзапиту
-- [INSERT WITH INTERVAL] Вставка даних з використанням обчислюваних дат (now() + INTERVAL)

## 📨 Select queries (OLAP & Analytics)
Select all entries (no WHERE, all fields)

-- [SELECT ALL] Базовий перегляд усіх записів таблиці

## Select public only info (no WHERE, specified fields - COUNT, SUM, AVG, MIN, MAX)

-- [BASIC AGGREGATION] Запит із використанням агрегатних функцій (COUNT, SUM, AVG, MIN, MAX) без GROUP BY

## API production example
GET /api/v1/resource/:id/analytics

-- [API ANALYTICS] Аналітична вибірка для конкретного ID (LEFT JOIN + GROUP BY + Агрегації)

## Some interesting examples (optional)
[ ] ORDER BY

[ ] LIMIT

[ ] OFFSET

[ ] JOIN (INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN, CROSS JOIN)

[ ] GROUP BY

[ ] HAVING

[ ] SUBQUERIES (in SELECT, WHERE, or HAVING)

-- [GROUP BY + HAVING + INNER JOIN] Групування, обчислення агрегатів та фільтрація груп через HAVING

-- [SUBQUERY IN WHERE + LEFT JOIN] Об'єднання таблиць із фільтрацією результатів через підзапит (наприклад, WHERE col > (SELECT AVG...))

-- [FULL OUTER JOIN / CROSS JOIN] Використання складних типів з'єднань або підзапиту в блоці SELECT

## 🔄 Update queries
Update some fields (WHERE)

-- [UPDATE WHERE] Оновлення полів із простим фільтром WHERE

Update fields returning values (WHERE, RETURNING)

-- [UPDATE RETURNING] Оновлення записів із поверненням змінених полів (RETURNING)

## Some interesting examples (optional)

-- [UPDATE WITH SUBQUERY IN SET] Оновлення поля значенням, обчисленим через підзапит

-- [UPDATE WITH SUBQUERY IN WHERE] Масове оновлення за умовою з підзапитом (IN / EXISTS)

## ⛔ Delete queries
Clear table (no WHERE)

-- [DELETE ALL] Очищення всієї таблиці

Delete with filter (WHERE)

-- [DELETE WHERE] Видалення записів за датою чи фільтром

Delete and return (WHERE, RETURNING)

-- [DELETE RETURNING] Видалення записів із поверненням інформації про вилучені рядки

Some interesting examples (optional)

-- [DELETE NOT EXISTS] Видалення застарілих даних за допомогою перевірки зв'язку NOT EXISTS

-- [DELETE WITH SUBQUERY IN] Видалення записів із фільтрацією через підзапит у WHERE