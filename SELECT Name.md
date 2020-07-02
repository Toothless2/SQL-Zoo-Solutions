# Tables
## world
|name|continent|capital
|-|-|-|

# Questions
1. Find the country that starts with a Y
```SQL
SELECT name FROM world WHERE name LIKE 'Y%'
```
2. Find the countries that end with a Y
```SQL
SELECT name FROM world WHERE name LIKE '%y'
```
3. Find all contires that contain an X in the name
```SQL
SELECT name FROM world WHERE name LIKE '%x%'
```
4. Find all countries that end with 'land'
```SQL
SELECT name FROM world WHERE name LIKE '%land'
```
5. Find all countries that start with C and end with ia
```SQL
SELECT name FROM world WHERE name LIKE 'C%ia'
```
6. Find countries containing a double o
```SQL
SELECT name FROM wold WHERE name LIKE 'oo'
```
7. Find countries that have 3 or more a's in the name
```SQL
SELECT name FROM wold WHERE name LIKE '%a%a%a%'
```
8. Find countries that have t as te second letter
```SQL
SELECT name FROM wold WHERE name LIKE '_t%'
```
9. Find countries that have two o's separated by two characters
```SQL
SELECT name FROM world WHERE name LIKE '%o__o%'
```
10. Find countires that have four character names
```SQL
SELECT name FROM world WHERE name LIKE '____'
```

---

## Harder Questions
11. Show the countries that have the same name as the capital
```SQL
SELECT name FROM world WHERE name = capital
```
12. Find the country where the capital is the country plus 'City'
```SQL
SELECT name FROM world WHERE capital = CONCAT(name, ' City')
```
13. Find the capital and the name where the capital incliudes the name of the country
```SQL
SELECT capital, name FROM world WHERE capital LIKE CONCAT('%', name, '%')
```
14. Find the capital and the name where the capital is an extansion of the country. e.g Include Mexico as capital is Mexico City but not Luxembourg
```SQL
SELECT capital, name FROM world WHERE capital LIKE CONCAT(name, '_%')
```
15. Show the name an the extension where the caputal is an extension of the name of the country
```SQL
SELECT capital, name FROM world WHERE capital LIKE CONCAT(name, '_%')
```

---
Previous: [[Select Basics]]
Next: [[SELECT from World]]