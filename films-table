/*List movies that have imdb score higher than 8 and have positive net profit */
SELECT f.title, (f.gross - f.budget) AS net_profit, r.imdb_score
FROM films f
INNER JOIN reviews r
ON f.id = r.film_id
WHERE imdb_score > 8
GROUP BY f.title, r.imdb_score,f.gross, f.budget
HAVING (f.gross-f.budget) > 0
ORDER BY net_profit DESC

/*Movies that have facebook likes above average facebook like*/
SELECT film_id, f.title, facebook_likes
FROM reviews r
LEFT JOIN films f
ON r.film_id = f.id
WHERE facebook_likes > (SELECT AVG(facebook_likes)
FROM reviews)
ORDER BY facebook_likes DESC;

/*List movies that have more than 1 actor*/
SELECT film_id, COUNT(role), role
FROM roles
GROUP BY film_id, role
HAVING COUNT(role) > 1
EXCEPT
SELECT film_id, COUNT(role), role
FROM roles
GROUP BY film_id, role
HAVING role = 'director'


/*Query for the movie names, gross, budget and directors that have an imdb score below 4. ORDER from worst to best in terms of score */
SELECT f.title,imdb_score, f.gross, f.budget, p.name
FROM reviews re 
INNER JOIN films f ON f.id = re.film_id
INNER JOIN roles ro ON f.id = ro.film_id
INNER JOIN people p ON ro.person_id = p.id
WHERE ro.role = 'director' AND re.imdb_score < 4
ORDER BY imdb_score ASC;

/*A6. Query for names of people along with the average imdb score of any film they ever took part in. Sort by average score in descending order.*/
SELECT p.name, AVG(imdb_score) as avg_score
FROM people p
INNER JOIN roles ro ON p.id = ro.person_id
INNER JOIN reviews re ON ro.film_id = re.film_id
INNER JOIN films f ON re.film_id = f.id
GROUP BY p.name
ORDER BY  AVG(imdb_score) DESC

SELECT p.name, AVG(imdb_score) as avg_score
FROM people p
INNER JOIN roles ro ON p.id = ro.person_id
INNER JOIN reviews re ON ro.film_id = re.film_id
GROUP BY p.name
ORDER BY  AVG(imdb_score) DESC


SELECT p.id, p.name, q.avg_score
FROM( 
SELECT person_id id, avg(imdb_score) avg_score
FROM roles ro 
JOIN reviews re USING(film_id)
GROUP BY person_id) q
INNER JOIN people p 
USING(id)
ORDER BY avg_score desc;

/*Q7. Query for name of person, their birthday and number of films this person was a part of.  
Try to use subquery in select instead of GROUP BY.*/

SELECT (
SELECT COUNT(film_id)
FROM roles r
WHERE r.person_id = p.id) AS num_films, name, birthdate
FROM people p

/*Get the name and birth date of the person born on November 11th, 1974. Remember to use ISO date format ('1974-11-11')! */
SELECT name, birthdate
FROM people
WHERE birthdate = '1974-11-11'; 
