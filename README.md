# A place to learn some SQL! 


Now, I particularly use PostgreSQL, using pgAdmin 4 dashboard.
You could use Mysql, or other sorts of databases that run sql queries. It doesn't matter.
However, there are slight differences in each and I suggest doing research to figure out which one is 
best for you and your situation.

Wanna download it? Go [here](https://www.postgresql.org).
Here's a great [website](https://sqlzoo.net) to learn many commands.

Upon setup, you will need to create a password. *DO NOT FORGET THAT PASSWORD*. You will need it to be able to use pg admin.


![alt text](https://thumbs.gfycat.com/PeacefulThoroughBrahmancow-size_restricted.gif)
##       Let's go....



# Using mockstaff.sql file 

You can run this query to see information about a specific table. Once it's downloaded and opened in postgreSQL.

```sql
SELECT * FROM company_divisions
```
The select is a function stating you want to select something. The star means to grab all of information stored
and company_divisions is a table that we have in our database. We want to extract information (all of it, hence the star) from
a specific table. 

```sql
SELECT * FROM company_regions
```
Returns us (all) the information from the table company regions!. Hence the * 
We did not place restrictions on what information we want requested. The star just says give us everything. 

Now you could imagine you could just change company_regions with any other table.


# Using the count_min_max.sql file and mockstaff.file should be already loaded.

Okay. We have a large table! What if you don't want to see  eveything at once... What if you wanted to see just a hint of what the whole table shows..

```sql
SELECT * FROM staff LIMIT 10
```
There you go. Using the LIMIT clause, you should see 10 rows from the table returned instead of 1000 that is in the table.

Now once you load the file and run the query say, ```Select * FROM staff``` 
A notification will appear in pgadmin showing how many rows are returned. It should say 1000.

BUT...

Let's say you forgot and it would be really costly to run the function again, but you still want to know how many staff employees you have. USE THE COUNT FUNCTION!
```sql
SELECT count(*) FROM staff 
```
This returns (you guessed it) 1000. 1000 for the number of employees. 

Ahhh. BUT HOW MANY OF THEM ARE WOMEN YOU ASK? 
NEVER FEAR SQL IS HERE! 
```sql
SELECT count(*) FROM staff GROUP BY gender
```
First things first. Gender has to be a column in the table(staff) for you to perform this. It has gender values as Male or Female. 
Second, GROUP BY is basically saying, yes give me the count from staff, but I want it to be returned in a different way. 
Count all these employees (hence the star!) but now I want you to count them by their gender and group them! 

AHA! We do get returned the right values, BUT!!!! It doesn't tell us which is which! 496 and 504 of what?
We can fix this. 
```sql
SELECT gender, count(*) FROM staff GROUP BY gender
```
Well why does this fix it. Well remember we wrote in our query to select on the count. In reality, this means return us just the count.
When we specify select gender, we are specifically stating to select it with our count as well.
Now we know that the number of males are 504 and females are 496.

- Getting the hang of it so far? If you come this far, I would like to recommend this [video](https://www.youtube.com/watch?v=yPu6qV5byu4). VERY efficient video about mysql, but many of the queries are the same. It is amazing. According to someone in the comments, they landed a job by watching that video.

Anyways...let's keep going.

## How many employees do we have per deparment? 
- - - - - - - - - - - - - - - - - - - - - - -
(TRY IT YOURSELF FIRST, SEE IF YOU CAN GET IT!)

- ANSWER BELOW 
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -
- - - - - - - - - - - - - - - - - - - - - - -






```sql
SELECT department, count(*) FROM staff GROUP BY department
```
Select department! Select their Count as well (for all employees, hence the star!). FROM my staff table inside my database.
THESE VALUES SELECTED WILL BE RETURNED!
NOW RETURN THEM TO ME BY GROUPING THEM BY THEIR SPECIFIC DEPARTMENT! 

Hows that for an all caps explanation? 22 rows for all 22 departments. We are too clever, aren't we?! 

## What is the highest salary of our employess..? 
```sql
SELECT max(salary) FROM staff
``` 
Yes! Very clever of you. Just change max with min and there you have it. The lowest salary will be returned! 
max is just one of the many "math" functions you could run.

Wanna see them at the same time? BUT you also want to see them based on employees in each department? You must be a very efficient person.

```sql
SELECT department, min(salary), max(salary)
FROM staff
GROUP BY department
``` 
Oh you must have wanted it specific to gender too? 

```sql
SELECT gender, min(salary), max(salary)
FROM staff
GROUP BY gender
``` 
There you have it. Go to your boss and claim you demand a higher salary! (Just kidding!)

Let's move on to statistical functions!
# Using statistics.sql file!

How much money is our company spending to pay our employees? Hey! Let's sum up all the salaries in the staff table!
```sql
SELECT sum(salary)
FROM staff
``` 
97.3 million paid per year across all staff. How much does each department pay in salary?

```sql
SELECT department, sum(salary)
FROM staff
GROUP BY department
``` 
22 rows for each of our 22 departments! What's the average?!

```sql
SELECT department, avg(salary)
FROM staff
GROUP BY department
``` 

Variance, Standard Deviations ?

```sql
SELECT department, var_pop(salary)
FROM staff
GROUP BY department
``` 
```sql
SELECT department, stddev_pop(salary)
FROM staff
GROUP BY department
``` 
We get way too many decimal places though, so lets round them and say we want 2 decimal places.
```sql
SELECT department, round(stddev_pop(salary),2)
FROM staff
GROUP BY department
``` 

# Using filter_group.sql file!
Filtering our data and grouping data.

Almost like booleans! If your familiar with coding. 
If not, its like adding clauses to our queries. Greater than, less than, equal to.

## Let's see all salaries greater then $100,000, by their name and department they work in.

```sql
SELECT last_name, department, salary
FROM staff
WHERE
salary > 100000
``` 
We used WHERE function, which is giving a restriction, or a specific request. 

OR we might want to see just one department.
just add ```WHERE department = 'Tools' ```
It is important to add the quotation marks, because tools in the database is loaded as a CHAR VAR which is a character variable, commonly known as a string in other coding languages.

If you have 2 restrictions? Just use  "AND" 

```sql
SELECT last_name, department, salary
FROM staff
WHERE
salary > 100000
AND
department = 'Tools'
``` 
We want only the department of tools and only the people with high salaries.

We can use OR as well! We will have some people in other departments. We will also have people in tools department with salaries lower than 100000 because we said OR. Give me this ... OR ... give me that.

```sql
SELECT last_name, department, salary
FROM staff
WHERE
department = 'Tools'
OR
salary > 100000
``` 

ALL DEPARMENTS that begin with letter B and sum of their salaries.
```sql
SELECT department, sum(salary)
FROM staff
WHERE
deparment LIKE 'B%'
GROUP BY department
``` 
WE used the LIKE function that basically says, WHERE something looks like "this". In our case B. The percent symbol is important here. Putting it before the B will change everything. We want the word to start with B and the % says and of the other letters could be arbitrary, as long as it starts with B, we want it returned. 

Beginning with letters Bo..?  ``` LIKE 'Bo%' ```

Baby or Beauty?  ```LIKE 'B%y' ```

# REFORMATTING data.  
- file: reformat.sql

We can reformat data to get it into a consisten format. You could change state names into their abbreviations to save space and have easier convenience of use.

```sql
SELECT DISTINCT department
FROM staff
```
DISTINCT allows us to return a specific in our query just once. There are many staff members in Beauty deparment. BUT
We do not want Beauty to appear 78 times. We want it to appear once, so we use DISTINCT.
Uppercase? Just use ``` UPPER(department) ```

Job title to combine with department name?

CONCAT IT.
```sql
SELECT
job_title || '-' || department
FROM staff
```
Concatenation is basically adding two things together without spaces in between. Concatenating String and HI = StringHI
So we want to separate them with a dash, hence the 
```sql
|| '-' ||
```
- We could also give names (titles) to columns we created.

```sql
SELECT
job_title || '-' || department title_dept
FROM staff
```
title_dept becomes the name of our column returned.
USE TRIM to remove whitespaces or extra characters.
```sql
SELECT
trim('   Sofware Engineer   ')
``` 
We cut out the leading and trailing whitespaces. 
Check it by 
```sql
SELECT length('   Software Engineer   ') 
``` 
with 
```sql
SELECT length(trim('   Software Engineer   ')) 
```
Length was reduced! :-)

Let's list all employees with title that begins with word assistant.
```sql
SELECT job_title
FROM staff
WHERE job_title like 'Assistant%'
```
Let's add a boolean, that will replace the WHERE clause
```sql
SELECT job_title, (job_title like '%Assistant%') is_asst
FROM staff
```
I added the first % before Assistant to get all queries where assistant might be the second word.
is_asst with return true if assistant is in the table abd false if not. 

# Extract those strings! 
- file: extract_string.sql

 ```sql
 SELECT
 'abcdefghijkl' test_string
 ```
 12 character string made. 
 Replace parts of a string with SUBSTRING function.
 
  ```sql
 SELECT
 SUBSTRING('abcdefghijkl' FROM 1 FOR 3) test_string
 ```
 Returns abc. 
 Using FROM 5, starts at 5th letter and prints everything on, inclusively. Index starts at 1, not 0!
 
 ```sql
 SELECT SUBSTRING(job_title FROM 10)
 FROM staff
 WHERE job_title LIKE 'Assistant%'
 ```
 We get the words that follow assistant. Because we start from the 10th index.
 
 ## Want to change the word assistant with Asst?
 
  ```sql
 SELECT OVERLAY(job_title PLACING 'Asst.' FROM 1 for 10)
 FROM staff
 WHERE job_title LIKE 'Assistant%'
 ```
 we lost the space in between Asst.Manager. We need to change the length of the string we replace from 10 to 9.
 
 # Filtering with regular expressions!
 - file: regular_expressions.sql
 
 ```sql
 SELECT job_title
 From staff
 WHERE job_title Like '%Assistant%'
 ```
 With this query, we noticed different levels of assistants...
 Let's select assistants at level 3 or 4. Similar to allows more expressive syntax. Separate III and IV by "OR" character.
 
  ```sql
 SELECT job_title
 From staff
 WHERE job_title SIMILAR TO '%Assistant%(III|IV)'
 ```
 Include list of jobs that includes the assistant 4 or 2 characters starting with I. 
 
  ```sql
 SELECT job_title
 From staff
 WHERE job_title SIMILAR TO '%Assistant I_'
 ```
 Adding the underscore is stating we only want one more character after the I. The only two options are II and IV, which
 is why these will be the only jobs the query returns.
 
 We can use square brackets as well. Jobs beginning with letters: E, P, OR S.
 
  ```sql
 SELECT job_title
 From staff
 WHERE job_title SIMILAR TO '[EPS]%'
 ```
 # Reformatting Numeric Data!
 - file: reformat_number.sql
 
 ```sql
 SELECT department, avg(salary)
 FROM staff
 GROUP BY department
 ```
 Avg salary produces more digits than necessary! 
 We could address this by using truncate function TRUNC. Does not round. It just ignores Decimals!
 
 ```sql
 SELECT department, trunc(avg(salary))
 FROM staff
 GROUP BY department
 ```
 
 Want to return the next largest integer? Use ceiling function ``` ceil(avg(salary)) ```.
 
 # SUBQUERIES in SELECT CLAUSES.
- Sub Queries can be used in three different parts of a select statement. In the list of values returned, in the From Clause and in the Where Clause.

```sql
SELECT
last_name, salary, department
FROM staff
```
Now, because we'll have multiple select statements within a single query we'll want to make sure the database can tell which table each value comes from. So to do this, we'll use a table alias and include that alias as a prefix for each value we'll return.
```sql
SELECT
s1.last_name, s1.salary, s1.department
FROM staff s1
```
Now, let's compare the salarys with the avg salary. We will use a nested select operator, as I like to call it.

```sql
SELECT
s1.last_name, s1.salary, s1.department, (SELECT round(avg(salary)) FROM staff s2 WHERE s2.department = s1.department)
FROM staff s1
```
Let me explain. 
Our inner query, calculated avg salary, but only uses rows where department is equal to department of employee we are currently looking at. You can see this adds an extra column. 
- We use a where clause that references a table in the top level query so that the subquery knows which row is referenced!

# SUBQUERIES in FROM CLAUSES.
- file: continuation from previous.


salary > 100000 is executive, by our assumption.
## We would like to find the average executive salary by department.

```sql
SELECT s1.department, round(avg(s1.salary))
FROM
  (SELECT department, salary 
  FROM staff
  WHERE salary > 100000) s1
GROUP BY s1.department
```
The inner SELECT is basically telling our outer SELECT to only select department and avg salary from the values that are returned from our inner select. (AFTER our FROM clause). 
 
 
# SUBQUERIES in WHERE CLAUSES. Useful for Comparisons within a single table.
WHEN USING SUBQUERIES use an alias, like I used previously with s1 and s2.

## Find department of person with highest salary. 

```sql
SELECT s1.department, s1.last_name, s1.salary
FROM staff s1
WHERE 
s1.salary = (SELECT max(s2.salary) FROM staff s2) #( This subquery- returns max salary)
```
Stanley, in the grocery deparment, making good money!


# JOINING THOSE TABLES! 
- file: joins.sql
- When working with SQL, we will sometimes need to retrieve data from multiple tables. For example, the Staff table includes a department for each employee. Departments are organized into divisions. Since we don't keep division information in the staff table, we have to look it up somewhere else.

```sql
SELECT * FROM company_divisions  
```
21 rows returned. Table has 2 columns. Departments and division.
Let's join staff and company_division.

```sql
SELECT s.last_name, s_department,cd.company_division
FROM staff s
JOIN company_divisions cd
ON s.department = cd.department
```
Returned 953 rows, but we should have 1000.  missing 47... mhm.

We use an outer join to return all rows. LEFT outer joins or right outer joins which depends on ordering of table.
```sql
SELECT s.last_name, s_department,cd.company_division
FROM staff s LEFT JOIN company_divisions cd
ON s.department = cd.department
```
Again, by left joining we're going to take all of the rows in the Staff table, even if there isn't a corresponding row in the Company Divisions table.

```sql
SELECT s.last_name, s_department,cd.company_division
FROM staff s LEFT JOIN company_divisions cd
ON s.department = cd.department
WHERE cd.company_division is NULL
```
They all come from the books department. 

# Creating a View.
- file: groupings.sql

```sql
SELECT s.*, cd.company_division, cr.company_regions
FROM staff s
LEFT JOIN company_divisions cd
ON s.department = cd.department
LEFT JOIN
company_regions cr
ON s.region_id = cr.region_id
``` 
What we have here is a select statement that uses two left joins and it selects all the rows from the staff table, it selects the company division, and the company regions name. It returns it as a single table.
Rather than retyping this if we want to see it, we create a view.

```sql
CREATE VIEW staff_div_reg AS
SELECT s.*, cd.company_division, cr.company_regions
FROM staff s
LEFT JOIN company_divisions cd
ON s.department = cd.department
LEFT JOIN
company_regions cr
ON s.region_id = cr.region_id
``` 
Want to view it?
```sql
SELECT count(*)
FROM staff_div_reg
``` 
We get a 1000. Check.
# Grouping and Totaling.
```sql
SELECT company_region, count(*)
FROM staff_div_reg
GROUP BY company_region
ORDER BY company_region # so we get it alphabetically.
``` 
If we want counts by both region and division. Use grouping sets.
```sql
SELECT company_division, company_region, count(*)
FROM staff_div_reg
GROUP BY 
GROUPING SETS (company_division,company_region)
ORDER BY company_region, company_division # so we get it alphabetically.
``` 
We also get totals by company division. We also get 47, with no name. That was the books department. It has no division.
Let's add gender.
```sql
SELECT company_division, company_region,gender,count(*)
FROM staff_div_reg
GROUP BY 
GROUPING SETS (company_division, company_region, gender)
ORDER BY company_region, company_division, gender # so we get it alphabetically.
``` 
 # WAYS TO GROUP DATA: ROLLUPS AND CUBES.
 - file: rollup-cube
 
 Now first, let's modify the staff division region view we created to include country code. To do that, I'm going to use the command CREATE OR REPLACE VIEW, and as the name implies, if this view doesn't exist, it will simply create it. If there is a version of this view that already exists, it'll replace that version with the version I'm about to specify.
 
 ```sql
 CREATE OR REPLACE VIEW staff_div_reg_country AS
 SELECT s.*, cd.company_division, cr.company_regions, cr.country
 FROM staff s
 LEFT JOIN company_divisions cd
 ON s.department = cd.department
 LEFT JOIN company_regions cr
 ON s.region_id = cr.region_id
 ```
 Let's select num of employees by company, region, country.
 
```sql
SELECT company_regions, country, count(*)
FROM staff_div_reg_country
GROUP BY company_regions, country
ORDER BY country, company_regions
```
Want totals for each country, use rollup in group by clause.
```sql
SELECT company_regions, country, count(*)
FROM staff_div_reg_country
GROUP BY 
ROLLUP(country,company_regions)
ORDER BY country, company_regions
```
 Now, for more advanced breakdowns, we can use the CUBE operation on the GROUP BY clause. This tells SQL to create all possible combinations of sets of grouping columns. For example, for each division, show results by region. So we will move the ORDER BY here and we'll remove ROLLUP, and we'll specify CUBE, and we're going to use not country, but we're going to use a cube of company_division.
 
 ```sql
SELECT company_division, company_regions, count(*)
FROM staff_div_reg_country
GROUP BY 
CUBE(company_division, company_regions)
```
Your cube needs to match your select for table names.


# FETCH FIRST. 
- file: fetch_first.sql

Working with large data sets, we might want to list employees with top ten salaries. 
Now, what I'm going to do is add a clause called fetch first. Now, fetch first works with the order by clause to sort and limit results. Fetch first is like the limit keyword, in that only a fixed number of rows are returned, but with fetch first, the ordering is performed before choosing the rows to return. So, I'll specify fetch first, 10 rows only, so this will return only 10 rows.
```sql
SELECT last_name, job_title, salary
FROM staff
ORDER BY salary DESC #DESC is return values in descending order
FETCH FIRST
10 ROWS ONLY
```
LIMIT would limit the rows and then perform operations (DESC), which is not what we want. 

Let's build aggregation query.
```sql
SELECT company_division, count(*)
FROM staff_div_reg_country
GROUP BY company_division
ORDER BY count(*)
```
Let's turn this into descending order
```sql
SELECT company_division, count(*)
FROM staff_div_reg_country
GROUP BY company_division
ORDER BY count(*) DESC
FETCH FIRST
5 ROWS ONLY
```

# Window Functions and Ordered Data.
- file: window.sql

Window functions allow us to make SQL statements about rows that are related to the current row during processing. This is somewhat like the way subqueries work. They let us do an operation that's related to the current row that SQL is processing. For example, instead of using a subquery to calculate an average salary for an employee's department, we can use a windowing function on rows called OVER PARTITION.

```sql
SELECT department, last_name, salary, avg(salary) OVER (PARTITION BY department)
FROM staff
```
So again, what I have is I've selected department, last_name, and salary, and I'm going to also display an average of salary for each department, and that's what the OVER PARTITION BY statement does.

```sql
SELECT company_region, last_name, salary, min(salary) OVER (PARTITION BY company_region)
FROM staff_div_reg
```
Min salary that is earned by based on region, not department. :-)

# Window Functions.
We could also select a set of attributes grouped by department and include the first value by department in each row using something called The First Value Function. 

```sql
SELECT department, last_name, salary,
first_value(salary) OVER (PARTITION BY department ORDER BY salary DESC)
FROM staff
```
I want the first value in the list of salaries, where its paritioned by department and in descending salary order.
In this case, first_value is acting like a max value, its the first value in descending salary list.

We could order by last name.
```sql
SELECT department, last_name, salary,
first_value(salary) OVER (PARTITION BY department ORDER BY last_name)
FROM staff
```
first_value is the salary of the first person in the table, after names are in alphabetical order.

# Window Functions: Rank.
It works with parition function to order results and assing a rank value based on the way paritition data is sorted.
```sql
SELECT department, last_name, salary,
rank() OVER (PARTITION BY department ORDER BY salary DESC)
FROM staff
```
Salaries are sorted and rank lists a number from 1 to the number of employees in the department. Ranking restarts by department and ranks by salary.

# LAG and LEAD.
- file: lead_lag.sql

We can reference rows RELATIVE to the currently processed rows. 
```sql
SELECT department, last_name, salary,
lag(salary) OVER (PARTITION BY department ORDER BY salary DESC)
FROM staff
```
lag refers to the row that came before a currently processed row.
```sql
SELECT department, last_name, salary,
lead(salary) OVER (PARTITION BY department ORDER BY salary DESC)
FROM staff
```
Lead will show rows that came after a currently processed row. 

# NTILE functions.
Sometimes we want to group rows into some number of buckets or ordered groups. We can use the ntiles function to assign buckets to rows. This allows us to easily calculate statistics like quartiles over sets of rows.

Ntile takes a number, and it will be the number of buckets that we want or ordered groups that we want
```sql
SELECT department, last_name, salary
ntile(4) OVER (PARTITION BY department ORDER BY salary DESC)
FROM staff
```
Top earners are assigned value 1.  Etc. ntile resets with each department.


# That's all! 
###### Pat yourself on the back. Give yourself a hug. Whatever suits you!
Thanks for following along. You have now learned ALOT. 
Remember:
1) Don't underestimate time needed to collect and prepare data.
2) Remember that an inner jointed SQL will return rows only when both tables have corresponding rows. If you want all the rows from one table even if there is not a corresponding row in the other table, then use an outer join.
3) Cubes, rollups, and grouping sets are useful when you need to produce cross-tabulations and subtotals.
4) Window Functions help us focus on sets of related rows such as all rows in a single department or company region. Window functions can help simplify select statements that would otherwise require subqueries.
5) SQL statements get complicated especially when using joins, subqueries, and complicated grouping and filtering clauses. Use views to capture this logic so that you can query the view instead of having to repeatedly type in long SQL statements. It's easy to make a mistake when typing in such statements so use views that you can test and verify.

