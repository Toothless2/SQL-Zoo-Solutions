# Tables
## stops
|id|name|
|-|-|

## route
|num|company|pos|stop|
|-|-|-|-|

pk for route : (num, company, pos)

---
# Questions
1. Number of stops in the database
```sql
SELECT COUNT(id) FROM stops
```
2. Find the id o the stop 'Craiglockhart'
```sql
SELECT id FROM stops WHERE name = 'Craiglockhart'
```
3. Give the id and the name for the stops on the '4' 'LRT' service
```sql
SELECT id, name FROM stops JOIN route ON (id = stop)
WHERE num = '4' AND company = 'LRT'
```
4. Show the routes that visit either 'London Road (149)' or 'Craiglockhart (53)' and using hacing only show where the number of stops is 2
```sql
SELECT company, num, COUNT(stop) FROM route WHERE stop IN (149, 53)
GROUP BY company, num
HAVING COUNT(stop) = 2
```
5. Using a self join show all routes going from 'Craiglockhart (53)' to 'London Road (149)'
```sql
SELECT a.company, a.num, a.stop AS 'start', b.stop AS 'end'
FROM route a JOIN route b ON (a.num=b.num AND a.company=b.company)
WHERE a.stop = 53 AND b.stop = 149
```
6. Reapeat [[Self Join#Questions#5 | Question 5]] however join in stops so that they may be refered to by name
```sql
SELECT a.comany, a.num, stopa.name AS 'start', stopb.name AS 'END'
FROM route a
	JOIN stops stopa ON (a.stop = stopa.id)
	JOIN route b ON (a.num=b.num AND a.company=b.company)
	JOIN stops stopb ON (b.stop = stopa.id)
WHERE stopa.name = 'Craiglockhart' AND stopb.name = 'London Road'
```
7. Give a list of services connecting stops 115 and 137
```sql
SELECT DISTINCT a.compay, a.num
FROM route a JOIN route b ON (a.num=b.num AND a.company=b.company)
WHERE a.stop = 115 AND b.stop = 137
```
8. Give a list of services connecting stops  'Craiglockhart' and 'Tollcross'
```sql
SELECT a.comany, a.num
FROM route a
	JOIN stops stopa ON (a.stop = stopa.id)
	JOIN route b ON (a.num=b.num AND a.company=b.company)
	JOIN stops stopb ON (b.stop = stopa.id)
WHERE stopa.name = 'Craiglockhart' AND stopb.name = 'Tollcross'
```
9. Give the distinct stops wich may be reached from 'Craiglockhart' by taking one bus including itself, offered by the 'LRT' company. Include company and bus number in the result
```sql
SELECT DISTINCT stopb.name, a.comany, a.num
FROM route a
	JOIN stops stopa ON (a.stop = stopa.id)
	JOIN route b ON (a.num=b.num AND a.company=b.company)
	JOIN stops stopb ON (b.stop = stopa.id)
WHERE stopa.name = 'Craiglockhart' AND a.company = 'LRT'
```
10. Find the routes involving two buses that can go from 'Craiglockhart' to 'Lochned'. Show the bus no and company for hte first bus, the name of the stop for the transfer, and the bus no and company for the second bus
```sql
SELECT s.num, s.company, s.name, e.num, e.company
FROM
	(
		SELECT a.num, a.company, stopb.name
		FROM route a
			JOIN route b ON (a.company=b.company AND a.num = b.num)
			JOIN stops stopa ON (a.stop = stopa.id)
			JOIN stops stopb ON (b.stop = stopb.id)
		WHERE stopa.name = 'Craiglockhart'
	) s
	JOIN
	(
		SELECT a.num, a.company, stopa.name
		FROM route a
			JOIN route b ON (a.company=b.company AND a.num = b.num)
			JOIN stops stopa ON (a.stop = stopa.id)
			JOIN stops stopb ON (b.stop = stopb.id)
		WHERE stopb.name = 'Lochned'
	) e
	ON s.name = e.name
ORDER BY s.num, s.name, e.num
```

---
Previous: [[COVID 19]]