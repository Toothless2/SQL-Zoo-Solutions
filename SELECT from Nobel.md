# Tables
## Nobel
|yr|subject|winner|
|-|-|-|

---
# Questions
1. Display prizes won in 1950
```sql
SELECT * FROM nobel WHERE yr = 1950
```
2. Show who won in 1962 for literature
```sql 
SELECT winner FROM nobel WHERE yr = 1962 AND subject = 'Literature'
```
3. Show the year and subject 'Albert Einstein' won
```sql
SELECT yr, subject FROM nobel WHERE winner = 'Albert Einstein'
```
4. Give the peace prize winners since 2000
```sql 
SELECT winner FROM nobel WHERE yr >= 2000 AND subject = 'Peace'
```
5. Show all details of literature prizes for 1980 to 1989 inclusive
```sql
SELECT * FROM nobel WHERE yr BETWEEN 1980 AND 1989 AND subject = 'Literature'
```
6. Show details of presidental winners ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter', and 'Barack Obama')
```sql
SELECT * FROM nobel WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter', 'Barack Obama')
```
7. Winners with a first name of 'John'
```sql
SELECT * FROM nobel WHERE winner LIKE 'John %'
```
8. Show all information of Phyiscs winners from 1980 and Chemisty winenrs from 1984
```sql
SELECT * FROM nobel WHERE (yr = 1980 AND subject = 'Physics') OR (yr = 1984 AND subject = 'Chemistry')
```
9. Show information for the year 1980 excluding Chemisty and Medicine
```sql
SELECT * FROM nobel WHERE yr = 1980 AND subject NOT IN ('Chemistry', 'Medicine')
```
10. Show information about Medicine prize winners before 1910 and Literature winners after and including 2004
```sql
SELECT * FROM nobel WHERE (yr < 1910 AND subject = 'Medicine') OR (yr >= 2004 AND subject = 'Literature')
```

---
## Harder Questions
11. Find details of the prize win by 'Peter Grünberg' (option + u for ¨)
```sql
SELECT * FROM nobel WHERE winner = 'Peter Grünberg'
```
12. Find details of prizes won by 'Eugene O'Neill'
```sql
SELECT * FROM nobel WHERE winner = 'Eugene O\'Neill'
```
13.  List the names starting with 'Sir' by year (most recent first) then name
```sql
SELECT * FROM nobel WHERE winner LIKE 'Sir %' ORDER BY yr DESC, winner
```
14. Show 1984 information ordered by subject then name; Showing 'Chemistry' and 'Physics Last'
```sql
SELECT * FROM nobel WHERE yr = 1984
	ORDER BY subject IN ('Chemistry', 'Physics'), subject, winner
```

---
Previous: [[SELECT from World]]
Next: [[SELECT within SELECT]]