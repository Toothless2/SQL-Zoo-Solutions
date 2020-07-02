# Tables

## nss
|ukprm|institution|subject|level|question|A_STRONGLY_DISAGREE|A_DISAGREE|A_NEUTRAL|A_AGREE|A_STRONGLY_AGREE|A_NA|CI_MIN|score|CI_MAX|respoinse|sample|aggregate|
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|

Data is prepresented as a percentage of response

---
# Questions
1. Show the percentage that responded as Stronly Agree for question 1, that go to Edinburgh Napier Univeristy, and study '(8) Computer Science'
```sql
SELECT A_STRONGLY_AGREE FROM nss
	WHERE question = 'Q01'
		AND institution = 'Edinburgh Napier Univeristy'
		AND subject =  '(8) Computer Science'
```
2. Show the institution and subject where the score is at least 100 for question 15
```sql
SELECT instituion, subject FROM nss WHERE question = 'Q15' AND score >= 100
```
3. Show the institution and score where the score is below 50 for computer science on question 15
```sql
SELECT institution, score FROM nss
	WHERE question = 'Q15'
		AND subject =  '(8) Computer Science'
		AND score < 50
```
4. Show the total number of responses for question 22 for '(8) Computer Science' and '(H) Creative Arts and Design'
```sql
SELECT subject, SUM(response) FROM nss
	WHERE question = 'Q22'
		AND subject IN ('(8) Computer Science', '(H) Creative Arts and Design')
	GROUP BY subject
```
5. Show the total number of Strongly Agree responses for question 22 for '(8) Computer Science' and '(H) Creative Arts and Design'
```sql
SELECT subject, SUM(A_STRONGLY_AGREE * response / 100) FROM nss
	WHERE question = 'Q22'
		AND subject IN ('(8) Computer Science', '(H) Creative Arts and Design')
	GROUP BY subject
```
6. Show the same information as [[Numeric Examples#Questions#1 | Quesiton 5]] however as a percentage to 0 dp
```sql
SELECT
	subject,
	ROUND(SUM(A_STRONGLY_AGREE * response / 100) / SUM(response) * 100, 0)
FROM
	nss
WHERE
	question = 'Q22'
	AND subject IN ('(8) Computer Science', '(H) Creative Arts and Design')
GROUP BY
	subject
```
7. Show the average score for question 22 where the institution has 'Manchester' in the name
```sql
SELECT
	institution,
	ROUND(SUM(score * response / 100) / SUM(response) * 100, 0) AS 'score'
WHERE
	question = 'Q22'
	AND instituion LIKE '%Manchester%'
GROUP BY institution
```
8. Show the institution, total smpel size, and the number of computing students for institutions in 'Manchester' for quetion 1
```sql
SELECT
	institution,
	SUM(sample),
	SUM((CASE WHEN subject = '(8) Computer Science' THEN sample ELSE 0 END)) AS comp
FROM
	nss
WHERE
	question = 'Q01'
	AND instituion LIKE '%Manchester%'
GROUP BY
	instituion
```

---
Previous: [[Using NULL]]
Next: [[Window Functions]]