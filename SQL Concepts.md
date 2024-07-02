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

