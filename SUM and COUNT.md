# Tables

## world
|name|continent|area|population|gdp|
|-|-|-|-|-|

---
# Questions
1. Show the totoal population of the world
```sql
SELECT SUM(population) FROM world
```
2. List all the continents
```sql
SELECT DISTINCT continent FROM world
```
or
```sql
SELECT continent FROM world GROUP BY continent
```
3. Total GDP of the African continent
```sql
SELECT SUM(gdp) FROM world WHERE continent = 'Africa'
```
4. How many contries have an area of at least 1,000,000
```sql
SELECT COUNT(name) FROM world WHERE area >= 1000000
```
5. Total population of Estona, Latvia, and Lithuania
```sql
SELECT SUM(population) FROM world WHERE name IN ('Estona', 'Latvia',  'Lithuania')
```
6. Show the number of countries in each continent
```sql
SELECT continent, COUNT(name) FROM world GROUP BY continent
```
7. For each continent show the continent and number of countries with populations of at least 10 million
```sql
SELECT continent, COUNT(name) FROM world WHERE population >= 10000000 GROUP BY continent
```
8. List continents that have a total population of at least 100 million
```sql
SELECT continent FROM world GROUP BY continent HAVING SUM(population) >= 100000000
```

---
Previous: [[SELECT within SELECT]]
Next: [[JOIN]]