# SELECT within SELECT Tutorial

This tutorial looks at how we can use SELECT statements within SELECT statements to perform more complex queries.

| name | continent | area | population | gdp |
| :--- | :--- | :--- | :--- | :--- |
| Afghanistan | Asia | 652230 | 25500100 | 20343000000 |
| Albania | Europe | 28748 | 2831741 | 12960000000 |
| Algeria | Africa | 2381741 | 37100000 | 188681000000 |
| Andorra | Europe | 468 | 78115 | 3712000000 |
| Angola | Africa | 1246700 | 20609294 | 100990000000 |
| ... |  |  |  |  |

## 1. Bigger than Russia

List each country **name** where the **population** is larger than that of 'Russia'.

```text
world(name, continent, area, population, gdp)
```

```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Romania')
```

## 2. Richer than UK

Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

The per capita GDP is the gdp/population

```sql
SELECT name FROM world
  WHERE continent='Europe' AND gdp/population >
     (SELECT gdp/population FROM world
      WHERE name='United Kingdom')
```

## 3. Neighbours of Argentina and Australia

List the **name** and **continent** of countries in the continents containing either **Argentina** or **Australia**. Order by name of the country.

```sql
SELECT name,continent
FROM world
WHERE continent IN (
  SELECT continent
  FROM world
  WHERE name IN ('Australia','Argentina'))
ORDER BY name
```

## 4. Between Canada and Poland

Which country has a population that is more than Canada but less than Poland? Show the name and the population.

```sql
select name, population from world where 
population > (select population from world where name = 'Canada') 
and 
population < (select population from world where name = 'Poland');
```

## 5. Percentages of Germany

Germany \(population 80 million\) has the largest population of the countries in Europe. Austria \(population 8.5 million\) has 11% of the population of Germany.

Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.

The format should be Name, Percentage for example:

| name | percentage |
| :--- | :--- |
| Albania | 3% |
| Andorra | 0% |
| Austria | 11% |
| ... | ... |

You can use the function [ROUND](https://sqlzoo.net/wiki/ROUND) to remove the decimal places.

You can use the function [CONCAT](https://sqlzoo.net/wiki/CONCAT) to add the percentage symbol.

```sql
SELECT name, CONCAT(CAST(ROUND(100*population/(SELECT population FROM world WHERE name = 'Germany'),0) as int), '%')
FROM world
WHERE continent = 'Europe'
```

  
 [To get a well rounded view of the important features of SQL you should move on to the next tutorial concerning aggregates.](https://sqlzoo.net/wiki/SUM_and_COUNT)

To gain an absurdly detailed view of one insignificant feature of the language, read on.

We can use the word `ALL` to allow &gt;= or &gt; or &lt; or &lt;=to act over a list. For example, you can find the largest country in the world, by population with this query:

```sql
SELECT name
  FROM world
 WHERE population >= ALL(SELECT population
                           FROM world
                          WHERE population>0)
```

You need the condition **population&gt;0** in the sub-query as some countries have **null** for population.

## 6. Bigger than every country in Europe

Which countries have a GDP greater than every country in Europe? \[Give the **name** only.\] \(Some countries may have NULL gdp values\)

```sql
SELECT name FROM world 
  WHERE gdp > ALL
   (SELECT gdp FROM world
    WHERE continent = 'Europe' 
      AND gdp IS NOT NULL)
```

We can refer to values in the outer SELECT within the inner SELECT. We can name the tables so that we can tell the difference between the inner and outer versions.

## 7. Largest in each continent

Find the largest country \(by area\) in each continent, show the **continent**, the **name** and the **area**:

```sql
select continent, name, area from world where area in 
(select MAX(area) from world group by continent)
```

The above example is known as a **correlated** or **synchronized** sub-query.

A correlated subquery works like a nested loop: the subquery only has access to rows related to a single record at a time in the outer query. The technique relies on table aliases to identify two different uses of the same table, one in the outer query and the other in the subquery.

One way to interpret the line in the **WHERE** clause that references the two table is “… where the correlated values are the same”.

In the example provided, you would say “select the country details from world where the population is greater than or equal to the population of all countries where the continent is the same”.

## 8. First country of each continent \(alphabetically\)

List each continent and the name of the country that comes first alphabetically.

```sql
SELECT continent, MIN(name) AS name
FROM world 
GROUP BY continent
ORDER by continent
```

```sql
SELECT continent,name FROM world x
  WHERE x.name <= ALL (
    SELECT name FROM world y
     WHERE x.continent=y.continent)
```

## 9. Difficult Questions That Utilize Techniques Not Covered In Prior Sections

Find the continents where all countries have a population &lt;= 25000000. Then find the names of the countries associated with these continents. Show **name**, **continent** and **population**.

```sql
SELECT name,continent,population FROM world x
  WHERE 25000000 >= ALL (
    SELECT population FROM world y
     WHERE x.continent=y.continent
       AND y.population>0)
```

## 10. Difficult Questions That Utilize Techniques Not Covered In Prior Sections

Some countries have populations more than three times that of any of their neighbours \(in the same continent\). Give the countries and continents.

```sql
SELECT name, continent FROM world x WHERE
 population > ALL
 (SELECT population*3 FROM world y
 WHERE y.continent = x.continent
 AND y.name != x.name)
```

