# SELECT from WORLD Tutorial

|  [Language:](https://sqlzoo.net/wiki/Special:MyLanguage/Project:Language_policy) | [**English**]()  • [日本語]() • [中文]() |
| :--- | :--- |


| name | continent | area | population | gdp |
| :--- | :--- | :--- | :--- | :--- |
| Afghanistan | Asia | 652230 | 25500100 | 20343000000 |
| Albania | Europe | 28748 | 2831741 | 12960000000 |
| Algeria | Africa | 2381741 | 37100000 | 188681000000 |
| Andorra | Europe | 468 | 78115 | 3712000000 |
| Angola | Africa | 1246700 | 20609294 | 100990000000 |
| ... |  |  |  |  |

  
 In this tutorial you will use the SELECT command on the table `world`:

## Introduction

[Read the notes about this table.](https://sqlzoo.net/wiki/Read_the_notes_about_this_table.) Observe the result of running this SQL command to show the name, continent and population of all countries.

```text
SELECT name, continent, population FROM world
```

```text
SELECT name, continent, population FROM world
```

## Large Countries

[How to use WHERE to filter records.](https://sqlzoo.net/wiki/WHERE_filters) Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

```text
SELECT name FROM world
WHERE population = 64105700
```

```text
SELECT name FROM world
WHERE population>200000000
```

## Per capita GDP

Give the `name` and the **per capita GDP** for those countries with a `population` of at least 200 million.

per capita GDP is the GDP divided by the population GDP/population

```text
SELECT name, gdp/population FROM world
  WHERE population > 200000000
```

## South America In millions

Show the `name` and `population` in millions for the countries of the `continent` 'South America'. Divide the population by 1000000 to get population in millions.

```text
SELECT name, population/1000000 FROM world
  WHERE continent='South America'
```

## France, Germany, Italy

Show the `name` and `population` for France, Germany, Italy

```text
SELECT name, population FROM world
  WHERE name IN ('France','Germany','Italy')
```

## United

Show the countries which have a `name` that includes the word 'United'

```text
SELECT name FROM world
  WHERE name LIKE '%United%'
```

## Two ways to be big

Two ways to be big: A country is **big** if it has an area of more than 3 million sq km or it has a population of more than 250 million.

Show the countries that are big by area or big by population. Show name, population and area.

```text
select name,population,area
from world
where area>3000000
or population>250000000
```

## One or the other \(but not both\)

Exclusive OR \(XOR\). Show the countries that are big by area \(more than 3 million\) or big by population \(more than 250 million\) but not both. Show name, population and area.

* Australia has a big area but a small population, it should be **included**.
* Indonesia has a big population but a small area, it should be **included**.
* China has a big population **and** big area, it should be **excluded**.
* United Kingdom has a small population and a small area, it should be **excluded**.

```text
select name, population,area
from world
where
(population>250000000 or area>3000000)
and not(population>250000000 and area>3000000)
```

## Rounding

Show the `name` and `population` in millions and the GDP in billions for the countries of the `continent` 'South America'. Use the [ROUND](https://sqlzoo.net/wiki/ROUND) function to show the values to two decimal places.

For South America show population in millions and GDP in billions both to 2 decimal places.

Divide by 1000000 \(6 zeros\) for millions. Divide by 1000000000 \(9 zeros\) for billions.

```text
SELECT name, ROUND(population/1000000,2),
             ROUND(gdp/1000000000,2)
  FROM world
 WHERE continent='South America'
```

## Trillion dollar economies

Show the `name` and per-capita GDP for those countries with a GDP of at least one trillion \(1000000000000; that is 12 zeros\). Round this value to the nearest 1000.

Show per-capita GDP for the trillion dollar countries to the nearest $1000.

```text
select name, ROUND(gdp/population,-3)
from world
where
gdp>1000000000000
```

## Name and capital have the same length

Greece has capital Athens.

Each of the strings 'Greece', and 'Athens' has 6 characters.

Show the name and capital where the name and the capital have the same number of characters.

* You can use the [LENGTH](https://sqlzoo.net/wiki/LENGTH) function to find the number of characters in a string

```text
SELECT name, LENGTH(name), continent, LENGTH(continent), capital, LENGTH(capital)
  FROM world
 WHERE name LIKE 'G%'
```

```text
SELECT name, capital
  FROM world
 WHERE LENGTH(name)=LENGTH(capital)
```

## Matching name and capital

The capital of Sweden is Stockholm. Both words start with the letter 'S'.

Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

* You can use the function [LEFT](https://sqlzoo.net/wiki/LEFT) to isolate the first character.
* You can use `<>` as the **NOT EQUALS** operator.

```text
SELECT name, LEFT(name,1), capital
FROM world
```

```text
SELECT name,capital
FROM world
WHERE LEFT(name,1)=LEFT(capital,1)
AND name<>capital
```

## All the vowels

**Equatorial Guinea** and **Dominican Republic** have all of the vowels \(a e i o u\) in the name. They don't count because they have more than one word in the name.

Find the country that has all the vowels and no spaces in its name.

* You can use the phrase `name NOT LIKE '%a%'` to exclude characters from your results.
* The query shown misses countries like Bahamas and Belarus because they contain at least one 'a'

```text
SELECT name
   FROM world
WHERE name LIKE 'B%'
  AND name NOT LIKE '%a%'
```

```text
SELECT name
  FROM world
WHERE name LIKE '%a%'
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
AND name NOT LIKE '% %'
```

## What Next

* [BBC QUIZ](https://sqlzoo.net/wiki/BBC_QUIZ)
* You can to continue practising the the same techniques and gain more experience of the basic skills on the Nobel table. [The `WHERE` statement using the `nobel` table.](https://sqlzoo.net/wiki/SELECT_from_Nobel_Tutorial)
* You can learn about nested statements, these are instructive and entertaining, but not essential for beginners. [Nested `SELECT` statements using the `world` table.](https://sqlzoo.net/wiki/SELECT_within_SELECT_Tutorial)

