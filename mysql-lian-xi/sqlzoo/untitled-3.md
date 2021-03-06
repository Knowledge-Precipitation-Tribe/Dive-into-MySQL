# SELECT from Nobel Tutorial

| nobel |  |  |
| :--- | :--- | :--- |
| yr | subject | winner |
| 1960 | Chemistry | Willard F. Libby |
| 1960 | Literature | Saint-John Perse |
| 1960 | Medicine | Sir Frank Macfarlane Burnet |
| 1960 | Medicine | Peter Madawar |
| ... |  |  |

## `nobel` Nobel Laureates

We continue practicing simple SQL queries on a single table.

This tutorial is concerned with a table of Nobel prize winners:

```text
nobel(yr, subject, winner)
```

Using the `SELECT` statement.

## 1. Winners from 1950

Change the query shown so that it displays Nobel prizes for 1950.

```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1960
```

```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

## 2. 1962 Literature

Show who won the 1962 prize for Literature.

```sql
SELECT winner
  FROM nobel
 WHERE yr = 1960
   AND subject = 'Physics'
```

```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature'
```

## 3. Albert Einstein

Show the year and subject that won 'Albert Einstein' his prize.

```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```

## 4. Recent Peace Prizes

Give the name of the 'Peace' winners since the year 2000, including 2000.

```sql
SELECT winner
FROM nobel
WHERE subject = 'Peace'
AND yr >= 2000
```

## 5. Literature in the 1980's

Show all details \(**yr**, **subject**, **winner**\) of the Literature prize winners for 1980 to 1989 inclusive.

```sql
SELECT yr,subject,winner
FROM nobel
WHERE subject = 'Literature'
AND yr BETWEEN 1980 AND 1989
```

## 6. Only Presidents

Show all details of the presidential winners:

* Theodore Roosevelt
* Woodrow Wilson
* Jimmy Carter
* Barack Obama

```sql
SELECT * FROM nobel
 WHERE yr = 1970
  AND subject IN ('Cookery',
                  'Chemistry',
                  'Literature')
```

```sql
SELECT * FROM nobel
 WHERE  winner IN ('Theodore Roosevelt',
  'Woodrow Wilson',
  'Jimmy Carter',
  'Barack Obama')
```

## 7. John

Show the winners with first name John

```sql
SELECT winner FROM nobel
  WHERE winner LIKE 'John %'
```

## 8. Chemistry and Physics from different years

Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984.

```sql
SELECT *
FROM nobel
WHERE (subject='physics' AND yr=1980) OR
      (subject='chemistry' AND yr=1984)
```

## 9. Exclude Chemists and Medics

Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine

```sql
SELECT *
FROM nobel
WHERE yr=1980 AND
  subject NOT IN ('Chemistry','Medicine')
```

## 10. Early Medicine, Late Literature

Show year, subject, and name of people who won a 'Medicine' prize in an early year \(before 1910, not including 1910\) together with winners of a 'Literature' prize in a later year \(after 2004, including 2004\)

```sql
SELECT *
FROM nobel 
WHERE (subject='Medicine' and yr <1910) OR
      (subject='Literature' AND yr>=2004)
```

## Harder Questions

## 11. Umlaut

Find all details of the prize won by PETER GRÜNBERG

```sql
SELECT *
FROM nobel 
WHERE winner in ('Peter Grünberg')
```

## 12. Apostrophe

Find all details of the prize won by EUGENE O'NEILL

You can't put a single quote in a quote string directly. You can use two single quotes within a quoted string.

```sql
SELECT *
FROM nobel 
WHERE winner in ('Eugene O''Neill')
```

## 13. Knights of the realm

Knights in order

List the winners, year and subject where the winner starts with **Sir**. Show the the most recent first, then by name order.

```sql
SELECT winner, yr, subject
FROM nobel 
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner
```

## 14. Chemistry and Physics last

The expression **subject IN \('Chemistry','Physics'\)** can be used as a value - it will be **0** or **1**.

Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.

```sql
SELECT winner, subject, subject IN ('Physics','Chemistry')
  FROM nobel
 WHERE yr=1984
 ORDER BY subject,winner
```

```sql
select winner, subject
from nobel
where yr=1984 
order by subject in ('Physics','Chemistry'),subject,winner
```

