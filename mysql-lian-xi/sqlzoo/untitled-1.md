# SELECT basics

|  [Language:](https://sqlzoo.net/wiki/Special:MyLanguage/Project:Language_policy) | [**English**]()  • [Deutsch]() • [español]() • [日本語]() • [中文]() |
| :--- | :--- |


| world |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- |
| name | continent | area | population | gdp |
| Afghanistan | Asia | 652230 | 25500100 | 20343000000 |
| Albania | Europe | 28748 | 2831741 | 12960000000 |
| Algeria | Africa | 2381741 | 37100000 | 188681000000 |
| Andorra | Europe | 468 | 78115 | 3712000000 |
| Angola | Africa | 1246700 | 20609294 | 100990000000 |
| .... |  |  |  |  |

## Introducing the `world` table of countries

The example uses a WHERE clause to show the population of 'France'. Note that strings \(pieces of text that are data\) should be in 'single quotes';

Modify it to show the population of Germany

```text
SELECT population FROM world
  WHERE name = 'France'
```

```text
SELECT population FROM world
  WHERE name = 'Germany'
```

## Scandinavia

Checking a list The word **IN** allows us to check if an item is in a list. The example shows the name and population for the countries 'Brazil', 'Russia', 'India' and 'China'.

Show the **name** and the **population** for 'Sweden', 'Norway' and 'Denmark'.

```text
SELECT name, population FROM world
  WHERE name IN ('Brazil', 'Russia', 'India', 'China');
```

```text
SELECT name, population FROM world
  WHERE name IN ('Sweden','Norway', 'Denmark');
```

## Just the right size

Which countries are not too small and not too big? `BETWEEN` allows range checking \(range specified is inclusive of boundary values\). The example below shows countries with an area of 250,000-300,000 sq. km. Modify it to show the country and the area for countries with an area between 200,000 and 250,000.

```text
SELECT name, area FROM world
  WHERE area BETWEEN 250000 AND 300000
```

```text
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```

* * You are ready for tutorial one:[SELECT statements with WHERE.](https://sqlzoo.net/wiki/SELECT_from_WORLD_Tutorial)

|  [Language:](https://sqlzoo.net/wiki/Special:MyLanguage/Project:Language_policy) | [**English**]()  • [Deutsch]() • [español]() • [日本語]() • [中文]() |
| :--- | :--- |


