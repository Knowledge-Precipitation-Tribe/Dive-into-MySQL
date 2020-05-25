# More JOIN operations

This tutorial introduces the notion of a join. The database consists of three tables `movie` , `actor` and `casting` .

| movie |  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **id** | title | yr | director | budget | gross |

| actor |  |
| :--- | :--- |
| **id** | name |

| casting |  |  |
| :--- | :--- | :--- |
| **movieid** | **actorid** | **ord** |

![](../../.gitbook/assets/image%20%28133%29.png)

[More details about the database.](https://sqlzoo.net/wiki/More_details_about_the_database.)

## 1. 1962 movies

List the films where the **yr** is 1962 \[Show **id**, **title**\]

```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```

## 2. When was Citizen Kane released?

Give year of 'Citizen Kane'.

```sql
SELECT yr 
FROM movie 
WHERE title='Citizen Kane'
```

## 3. Star Trek movies

List all of the Star Trek movies, include the **id**, **title** and **yr** \(all of these movies include the words Star Trek in the title\). Order results by year.

```sql
SELECT id,title, yr FROM movie
 WHERE title LIKE 'Star Trek%'
 ORDER BY yr
```

## 4. id for actor Glenn Close

What **id** number does the actor 'Glenn Close' have?

```sql
SELECT id FROM actor
  WHERE name= 'Glenn Close'
```

## 5. id for Casablanca

What is the **id** of the film 'Casablanca'

```sql
SELECT id 
FROM movie 
WHERE title='Casablanca'
```

[Get to the point](https://sqlzoo.net/wiki/Get_to_the_point)

## 6. Cast list for Casablanca

Obtain the cast list for 'Casablanca'.

The cast list is the names of the actors who were in the movie.

Use **movieid=11768**, \(or whatever value you got from the previous question\)

```text
SELECT name
  FROM casting, actor
  WHERE movieid=(SELECT id 
             FROM movie 
             WHERE title='Casablanca')
    AND actorid=actor.id
```

## 7. Alien cast list

Obtain the cast list for the film 'Alien'

```text
SELECT name
  FROM movie, casting, actor
  WHERE title='Alien'
    AND movieid=movie.id
    AND actorid=actor.id
```

## 8. Harrison Ford movies

List the films in which 'Harrison Ford' has appeared

```sql
SELECT title
  FROM movie, casting, actor
 WHERE name='Harrison Ford'
    AND movieid=movie.id
    AND actorid=actor.id
```

## 9. Harrison Ford as a supporting actor

List the films where 'Harrison Ford' has appeared - but not in the starring role. \[Note: the **ord** field of casting gives the position of the actor. If ord=1 then this actor is in the starring role\]

```sql
SELECT title
  FROM movie, casting, actor
 WHERE name='Harrison Ford'
    AND movieid=movie.id
    AND actorid=actor.id
  AND ord!=1
```

## 10. Lead actors in 1962 movies

List the films together with the leading star for all 1962 films.

```sql
SELECT title, name
  FROM movie, casting, actor
 WHERE yr=1962
    AND movieid=movie.id
    AND actorid=actor.id
    AND ord=1
```

## 11. Busy years for Rock Hudson

Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

```sql
SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
where name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2
```

## 12. Lead actor in Julie Andrews movies

List the film title and the leading actor for all of the films 'Julie Andrews' played in.

Did you get "Little Miss Marker twice"?

Julie Andrews starred in the 1980 remake of Little Miss Marker and not the original\(1934\).

Title is not a unique field, create a table of IDs in your subquery

```sql
SELECT title, name
  FROM movie, casting, actor
  WHERE movieid=movie.id
    AND actorid=actor.id
    AND ord=1
    AND movieid IN
    (SELECT movieid FROM casting, actor
     WHERE actorid=actor.id
     AND name='Julie Andrews')
```

## 13. Actors with 15 leading roles

Obtain a list, in alphabetical order, of actors who've had at least 15 **starring** roles.

```sql
SELECT name
    FROM casting JOIN actor
      ON  actorid = actor.id
    WHERE ord=1
    GROUP BY name
    HAVING COUNT(movieid)>=15
```

## 14. 

List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

```sql
  SELECT title, COUNT(actorid)
  FROM casting,movie                
  WHERE yr=1978
        AND movieid=movie.id
  GROUP BY title
  ORDER BY 2 DESC,1 ASC
```

## 15. 

List all the people who have worked with 'Art Garfunkel'.

```sql
SELECT DISTINCT d.name
FROM actor d JOIN casting a ON (a.actorid=d.id)
   JOIN casting b on (a.movieid=b.movieid)
   JOIN actor c on (b.actorid=c.id 
                and c.name='Art Garfunkel')
  WHERE d.id!=c.id
```

