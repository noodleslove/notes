### ALIASES

#### COLUMNS

```sql
SELECT name AS city_name
FROM city;
```

#### TABLES

```sql
SELECT co.name, ci.name
FROM city AS ci
JOIN country AS co
  ON ci.country_id = co.id;
```

### FILTERING THE OUTPUT

#### COMPARISON OPERATORS

Fetch names of cities that have a rating above 3:

```sql
SELECT name
FROM city
WHERE rating > 3;
```

Fetch names of cities that are neither Berlin nor Madrid:

```sql
SELECT name
FROM city
WHERE name != 'Berlin'
  AND name != 'Madrid';
```

#### TEXT OPERATORS

Fetch names of cities that start with a 'P' or end with an 's':

```sql
SELECT name
FROM city
WHERE name LIKE 'P%'
  OR name LIKE '%s';
```

Fetch names of cities that start with any letter followed by 'ublin' (like Dublin in Ireland or Lublin in Poland):

```sql
SELECT name
FROM city
WHERE name LIKE '_ublin';
```

#### OTHER OPERATORS

Fetch names of cities that have a population between 500K and 5M:

```sql
SELECT name
FROM city
WHERE population BETWEEN 500000 AND 5000000;
```

Fetch names of cities that don't miss a rating value:

```sql
SELECT name
FROM city
WHERE rating IS NOT NULL;
```

Fetch names of cities that are in countries with IDs 1, 4, 7, or 8:

```sql
SELECT name
FROM city
WHERE country_id IN (1, 4, 7, 8);
```

### QUERYING MULTIPLE TABLES

#### INNER JOIN

**`JOIN`** (or explicitly **`INNER JOIN`**) returns rows that have matching values in both tables.

```sql
SELECT city.name, country.name
FROM city
[INNER] JOIN country
  ON city.country_id = country.id;
```

#### LEFT JOIN

**`LEFT JOIN`** returns all rows from the left table with corresponding rows from the right table. If there's no matching row, **`NULL`**s are returned as values from the second table.

```sql
SELECT city.name, country.name
FROM city
LEFT JOIN country
  ON city.country_id = country.id;
```

#### RIGHT JOIN

**`[RIGHT JOIN](https://learnsql.com/blog/right-join/)`** returns all rows from the right table with corresponding rows from the left table. If there's no matching row, **`NULL`**s are returned as values from the left table.

```sql
SELECT city.name, country.name
FROM city
RIGHT JOIN country
  ON city.country_id = country.id;
```

#### FULL JOIN

**`FULL JOIN`** (or explicitly **`FULL OUTER JOIN`**) returns all rows from both tables – if there's no matching row in the second table, **`NULL`**s are returned.

```sql
SELECT city.name, country.name
FROM city
FULL [OUTER] JOIN country
  ON city.country_id = country.id;
```

#### CROSS JOIN

**`CROSS JOIN`** returns all possible combinations of rows from both tables. There are two syntaxes available.

```sql
SELECT city.name, country.name
FROM city
CROSS JOIN country;
```

```sql
SELECT city.name, country.name
FROM city, country;
```

#### NATURAL JOIN

**`NATURAL JOIN`** will join tables by all columns with the same name.

```sql
SELECT city.name, country.name
FROM city
NATURAL JOIN country;
```

**`NATURAL JOIN`** used these columns to match rows: **`city.id`**, **`city.name`**, **`country.id`**, **`country.name`**.  
**`NATURAL JOIN`** is very rarely used in practice.

### AGGREGATION AND GROUPING

`GROUP BY` **groups** together rows that have the same values in specified columns. It computes summaries (aggregates) for each unique combination of values.

#### AGGREGATE FUNCTIONS

- `avg(expr)` − average value for rows within the group
- `count(expr)` − count of values for rows within the group
- `max(expr)` − maximum value within the group
- `min(expr)` − minimum value within the group
- `sum(expr)` − sum of values within the group

### SUBQUERIES

A subquery is a query that is nested inside another query, or inside another subquery. There are different types of subqueries.

#### SINGLE VALUE

The simplest subquery returns exactly one column and exactly one row. It can be used with comparison operators `=`, `<`, `<=`, `>`, or `>=`.

This query finds cities with the same rating as Paris:

```sql
SELECT name
FROM city
WHERE rating = (
  SELECT rating
  FROM city
  WHERE name = 'Paris'
);
```

#### MULTIPLE VALUES

A subquery can also return multiple columns or multiple rows. Such subqueries can be used with operators `IN`, `EXISTS`, `ALL`, or `ANY`.

This query finds cities in countries that have a population above 20M:

```sql
SELECT name
FROM city
WHERE country_id IN (
  SELECT country_id
  FROM country
  WHERE population > 20000000
);
```

#### CORRELATED

A correlated subquery refers to the tables introduced in the outer query. A correlated subquery depends on the outer query. It cannot be run independently from the outer query.

This query finds cities with a population greater than the average population in the country:

```sql
SELECT *
FROM city main_city
WHERE population > (
  SELECT AVG(population)
  FROM city average_city
  WHERE average_city.country_id = main_city.country_id
);
```

This query finds countries that have at least one city:

```sql
SELECT name
FROM country
WHERE EXISTS (
  SELECT *
  FROM city
  WHERE country_id = country.id
);
```

### SET OPERATIONS

Set operations are used to combine the results of two or more queries into a single result. The combined queries must return the same number of columns and compatible data types. The names of the corresponding columns can be different

#### UNION

**`UNION`** combines the results of two result sets and removes duplicates. **`UNION ALL`** doesn't remove duplicate rows.

This query displays German cyclists together with German skaters:

```sql
SELECT name
FROM cycling
WHERE country = 'DE'
UNION / UNION ALL
SELECT name
FROM skating
WHERE country = 'DE';
```

#### UNION

**`UNION`** combines the results of two result sets and removes duplicates. **`UNION ALL`** doesn't remove duplicate rows.

This query displays German cyclists together with German skaters:

```sql
SELECT name
FROM cycling
WHERE country = 'DE'
UNION / UNION ALL
SELECT name
FROM skating
WHERE country = 'DE';
```

### Managing SQL constraints![Copy Icon](https://www.cockroachlabs.com/images/icons/copy-icon.svg)

#### [ADD CONSTRAINT](https://www.cockroachlabs.com/docs/stable/alter-table#add-constraint)

Add a key, check, or unique constraint to a column.

```sql
ALTER TABLE users
ADD CONSTRAINT id_name_unique UNIQUE (id, name);
```

#### [DROP CONSTRAINT](https://www.cockroachlabs.com/docs/stable/alter-table#drop-constraint)

Remove a constraint from a column.

```sql
ALTER TABLE users
DROP CONSTRAINT id_name_unique;
```

#### [ALTER COLUMN](https://www.cockroachlabs.com/docs/stable/alter-table#alter-column)

Add or remove `DEFAULT` and `NOT NULL` constraints, change datatypes.

```sql
ALTER TABLE subscriptions
ALTER COLUMN newsletter SET NOT NULL;
```

### Inserting data![Copy Icon](https://www.cockroachlabs.com/images/icons/copy-icon.svg)

#### [INSERT INTO … VALUES](https://www.cockroachlabs.com/docs/stable/insert)

Insert rows with specified values into a table.

```sql
INSERT INTO users (name, city)
VALUES('Alice', 'New York');
```
#### [INSERT INTO … SELECT](https://www.cockroachlabs.com/docs/stable/insert#insert-from-a-select-statement)

Insert rows into a table from the results of a query.

```sql
INSERT INTO drivers (id, city, name, address) SELECT id, city, name, address FROM users WHERE name IN ('Anita Atkinson', 'Devin Jordan');
```