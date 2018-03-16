

## Basic Select

```sql
SELECT * FROM CITY WHERE COUNTRYCODE = 'USA' AND POPULATION > 100000;
```

```sql
SELECT * FROM city;
```

Use `DISTINCT` and `%`.

```sql
SELECT DISTINCT city FROM sql WHERE id % 2 = 0;
```

Use `LENGTH()`, `MIN()`, `ORDER BY` and `LIMIT`.

```sql
SELECT city,LENGTH(city) FROM station WHERE LENGTH(city) = (
    SELECT MIN(LENGTH(city)) FROM station
) ORDER BY city LIMIT 1;

SELECT city,LENGTH(city) FROM station WHERE LENGTH(city) = (
    SELECT MAX(LENGTH(city)) FROM station
) ORDER BY city LIMIT 1;
```

USE `DISTINCT` and `REGEXP`.

```sql
SELECT DISTINCT city FROM station WHERE city REGEXP '^[aeiou]';
SELECT DISTINCT city FROM station WHERE city REGEXP '[aeiou]$';
SELECT city FROM station WHERE city REGEXP '^[aeiou].*[aeiou]$';
SELECT DISTINCT city FROM station WHERE city NOT REGEXP '^[aeiou].*[aeiou]$';
```

Use `ORDER BY`, `ASC`, `DESC` and `RIGHT()`.

```sql
SELECT name FROM students WHERE marks > 75 ORDER BY RIGHT(name, 3) ASC, id ASC;
```

## Advanced Search

Use `CASE...WHEN...THEN...ELSE...END`.

```sql
SELECT 
  CASE 
    WHEN a + b <= c OR a + c <= b OR b + c <= a THEN 'Not A Triangle' 
    WHEN a=b AND b=c THEN 'Equilateral' 
    WHEN a=b OR a=c OR b=c THEN 'Isosceles' 
    ELSE 'Scalene' 
  END 
FROM triangles;
```

Use `CONCAT()`, `LEFT()` and `GROUP BY`. If `GROUP BY` happened, make sure you have `GROUP BY` or aggregation function
in `SELECT`. If you want to filter `aggregation` function, use `HAVING` NOT `WHERE`.

```sql
SELECT CONCAT(name, '(', LEFT( occupation, 1), ')')
FROM occupations
ORDER BY name;

SELECT CONCAT('There are a total of ', COUNT(*), ' ', lower(occupation), 's.')
FROM occupations
GROUP BY occupation
ORDER BY COUNT(*), occupation;
```

## Aggregation Function

Use `SUM()` and `LIKE`.

```sql
SELECT SUM(population) FROM city WHERE district LIKE 'California';
```

USE `AVG()` and `FLOOR()`.

```sql
SELECT FLOOR(AVG(POPULATION)) FROM CITY;
```

USE `ROUND()`.

```sql
select round(sum(lat_n), 4) from station where lat_n > 38.7880 and lat_n < 137.2345;
```

## Basic Join


[Inner/Left/Right/Outer Join](https://www.youtube.com/watch?v=KTvYHEntvn8)

```sql

```