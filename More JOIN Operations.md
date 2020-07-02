# Tables
## movie
|id|title|yr|director|budget|gross|
|-|-|-|-|-|-|

## actor
|id|name|
|-|-|

## casting
|movieid|actorid|ord|
|-|-|-|

## Relations
movie -> casting : related by `movie.id` = `casting.movieid`
actor -> casting : related by `actor.id` = `casting.actorid`
movie -> actor : related by (director only) `movie.director` = `actor.id`

---
# Questions
1. Show id and title of films with the year 1962
```sql
SELECT id, title FROM movie WHERE yr = 1962
```
2. Give the year 'Citizen Kane' released
```sql
SELECT yr FROM moive WHERE title = 'Citizen Kane'
```
3. List all Star Trek movies id, title, and year ordered by year
```sql
SELECT id, title, yr FROM movie WHERE title LIKE 'Star Trek%' ORDER BY yr
```
4. Show the id for actor 'Glen Close'
```sql
SELECT id FROM actor WHERE name = 'Glen Close'
```
5. List the film id for 'Casablanca'
```sql
SELECT id FROM movie WHERE title = 'Casablanca'
```
6. What is the cast list for the film with the id 11768
```sql
SELECT name FROM casting
	JOIN actor ON id = actorid
	WHERE movieid = 11768
```
7. Get the cast list for 'Alien'
```sql
SELECT name FROM actor
	JOIN casting ON (actor.id = casting.actorid)
	JOIN movie ON (movie.id = casting.movieid)
	WHERE title = 'Alien'
```
8. Show all films where 'Harrison Ford' has appeared
```sql
SELECT title FROM movie
	JOIN casting ON (movie.id = casting.movieid)
	JOIN actor ON (casting.actorid = actor.id)
	WHERE actor.name = 'Harrison Ford' 
```
9. Show all films where 'Harrison Ford' has appeared but not as a lead role (ord != 1)
```sql
SELECT title FROM movie
	JOIN casting ON (movie.id = casting.movieid)
	JOIN actor ON (casting.actorid = actor.id)
	WHERE actor.name = 'Harrison Ford' AND ord <> 1
```
or
```sql
SELECT title FROM movie
	JOIN casting ON (movie.id = casting.movieid AND ord <> 1)
	JOIN actor ON (casting.actorid = actor.id)
	WHERE actor.name = 'Harrison Ford'
```
10. List films and leading actors for all films in 1962
```sql
SELECT title, name FROM movie
	JOIN casting ON (movie.id = casting.movieid AND ord = 1)
	JOIN actor ON (casting.actorid = actor.id)
	WHERE yr = 1962
```

---
## Harder Questions
11. Show the year and numbers of movies made when 'Rock Hudson' made more than 2 movies in one year
```sql
SELECT yr, COUNT(title) FROM movie
	JOIN casting ON (movie.id = casting.movieid)
	JOIN actor ON (casting.actorid = actor.id)
	WHERE name = 'Rock Hudson'
	GROUP BY yr
	HAVING COUNT(title) > 2 
```
12. List all films actress 'Julie Andrews' played in and the lead actor
```sql
SELECT title FROM movie
	JOIN casting ON (movie.id = casting.movieid AND ord = 1)
	JOIN actor ON (casting.actorid = actor.id)
	WHERE movieid = 
		(SELECT movieid FROM casting WHERE actorid = 
			(SELECT id FROM actor WHERE name = 'Julie Andrews'))
```
13. Obtain a list of actors with at least 15 lead roles
```sql
SELECT name FROM casting
	JOIN actor ON actorid = id
	WHERE ord = 1
	GROUP BY actorid
	HAVING COUNT(movieid) >= 15
```
14. List the films released in the year 1978 ordered by the number od actors in the cast then by the title
```sql
SELECT title, COUNT(actorid) FROM movie
	JOIN casting ON id = movieid
	WHERE yr = 1978
	GROUP BY movieid
	ORDER BY COUNT(actorid) DESC, title
```
15. List all the people that have worked with 'Art Garfunkel'
```sql
SELECT name FROM actor
	JOIN casting ON actorid = id
	WHERE name <> 'Art Garfunkel'
		movieid IN 
			(SELECT movieid FROM casting WHERE actorid = 
				(SELECT id FROM actor WHERE name = 'Art Garfunkel'))
```

---
Previous: [[JOIN]]
Next: [[Using NULL]]

