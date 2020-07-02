# Tables
## teacher
|id|dept|name|phone|mobile|
|-|-|-|-|-|

## dept
|id|name|
|-|-|

# Questions
1. List teachers who have NULL for their department
```SQL
SELECT name FROM teacher WHERE dept IS NULL
```

2. Note the inner join misses teahcer with no dept
```SQL
SELECT teacher.name, dept.name FROM teacher JOIN dept ON teacher.id = dept.id
```

3. Use a differnt join so that all teachers are listed even if they dont have a dept
```SQL
SELECT teacher.name, dept.name FROM teacher LEFT JOIN dept ON teacher.id = dept.id
```

4. Use a differnt join so that all departmets are listed even if they dont have a teacher
```SQL
SELECT teacher.name, dept.name FROM teacher RIGHT JOIN dept ON teacher.id = dept.id
```

5. Use `COALESCE` function to print teachers mobile numbers, if they do not have a number display '07968 444 2266'
``` SQL
SELECT name, COALESCE(mobile, '07968 444 2266') FROM teacher
```

6. Ue the `COALESCE` function to display all teachers with departents, where there is no department display 'None'
```SQL
SELECT teacher.name, COALESCE(dept.name, 'None') FROM teacher LEFT JOIN dept ON teacher.id = dept.id 
```

7. Use `COUNT` to show the number of teachers and the number of mobile phones
```SQL
SELECT COUNT(id), COUNT(mobile) FROM teacher
```

8. Use `COUNT` and `GROUP BY dept.name` to show eacher department and the number of staff. Ensure the all departments are listed
```SQL
SELECT dept.name, COUNT(teacher.id) FROM dept LEFT JOIN teacher ON (dept.id = teacher.dept) GROUP BY dept.name
```

9. Use `CASE` to show the name of each teacher follow by 'Sci' if the teacher is in dept 1  or 2 and 'Art' otherwise
```SQL
SELECT
	name,
	CASE WHEN dept IN (1, 2) THEN
		'Sci'
	ELSE
		'Art'
	END
FROM teacher
```

10. Use `CASE` to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, 'Art' if they are in 3, and 'None' otherwise
```SQL
SELECT
	name,
	CASE WHEN dept IN (1, 2) THEN
		'Sci'
	WHEN dept = 3 THEN
		'Art'
	ELSE
		'None'
	END
FROM teacher
```