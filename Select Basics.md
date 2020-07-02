# Tables
## world
|name|continent|area|population|gdp|
|-|-|-|-|-|

# Questions
1. Show the population of 'Germany'
```SQL
SELECT population FROM world WHERE name = 'Germany'
```
2. Show the name and population for 'Sweden', 'Norway', and 'Denmark' using  `IN`
```SQL
SELECT name, population FROM world WHERE name IN ( 'Sweden', 'Norway', 'Denmark')
```

3. Show countries `BETWEEN` 200,000 and 250,000 area (incusive)
```SQL
SELECT name, area FROM world WHERE area BETWEEN 200000 AND 250000
```

---

Next: [[SELECT Name]]