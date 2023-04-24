# LeetCode_SQL_Solutions
Solutions to SQL problems on LeetCode

### 1) Customers Who Never Order

https://leetcode.com/problems/customers-who-never-order/


select name as Customers

from customers

left join orders

on Customers.id = Orders.customerId

where customerId IS NULL;

### 2) Combine Two Tables

https://leetcode.com/problems/combine-two-tables/


SELECT firstName , lastName , city , state

FROM Person

LEFT JOIN Address

ON Person.personId = Address.personId;

### 3) Number of Unique Subjects Taught by Each Teacher

https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/

SELECT ROUND(SUM(i1.tiv_2016),2) AS tiv_2016 

FROM Insurance i1

INNER JOIN Insurance i2

ON i1.pid = i2.pid

WHERE (i1.lat , i1.lon) NOT IN (
  
  SELECT lat , lon 
  FROM Insurance 
  WHERE pid != i2.pid

) 

AND i1.tiv_2015 IN(

  SELECT tiv_2015 
  FROM Insurance 
  WHERE pid != i2.pid
)




SELECT teacher_id , COUNT( DISTINCT subject_id ) as cnt

FROM Teacher

GROUP BY teacher_id;

### 4) Rising Temperature

https://leetcode.com/problems/rising-temperature/

SELECT Weath1.id 

FROM Weather Weath1, Weather Weath2

WHERE dateDiff(Weath1.recordDate, Weath2.recordDate) = 1 AND Weath1.temperature  > Weath2.temperature

### 5) Big Countries

https://leetcode.com/problems/big-countries/

SELECT name, population , area    

FROM World 

WHERE area >= 3000000 OR population >= 25000000


### 6) Duplicate Emails

https://leetcode.com/problems/duplicate-emails/

SELECT email as Email

FROM Person 

GROUP BY email

HAVING COUNT(email) > 1

### 7) Sales Person

https://leetcode.com/problems/sales-person/

SELECT name 

FROM salesperson

WHERE sales_id NOT IN (

  SELECT sales_id

  FROM orders

  LEFT JOIN Company  

  ON orders.com_id = Company.com_id 

  WHERE name = 'RED'

)

### 8) Find Customer Referee

https://leetcode.com/problems/find-customer-referee/

SELECT name 

FROM Customer

WHERE referee_id IS NULL OR referee_id !=2

### 9) Find Followers Count

https://leetcode.com/problems/find-followers-count/

SELECT user_id , COUNT(follower_id) as followers_count

FROM Followers 

GROUP BY user_id 

ORDER BY user_id 

### 10) Triangle Judgement

https://leetcode.com/problems/triangle-judgement/

SELECT x,y,z,

CASE 

  WHEN (x+y > z AND y+z > x AND x+z > y) THEN 'Yes'ELSE 'No'

END AS triangle

FROM Triangle;

### 11) Employee Bonus

https://leetcode.com/problems/employee-bonus/

SELECT name , bonus 

FROM Employee

LEFT JOIN Bonus

ON Employee.empId = Bonus.empId 

WHERE bonus < 1000 OR bonus IS NULL

### 12) Employees Earning More Than Their Managers

https://leetcode.com/problems/employees-earning-more-than-their-managers/

SELECT e1.name  AS Employee 

FROM Employee  e1

LEFT JOIN Employee e2

ON e1.managerId = e2.id 

WHERE e1.salary > e2.salary


### 13) Patients With a Condition

https://leetcode.com/problems/patients-with-a-condition/

SELECT * 

FROM Patients

WHERE conditions  LIKE 'DIAB1%' OR conditions  LIKE '% DIAB1%'                     # Note the space before DIAB1

### 14) Customer Who Visited but Did Not Make Any Transactions

https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/

SELECT customer_id, COUNT(visit_id) AS count_no_trans 

FROM Visits

WHERE visit_id NOT IN

 (

  SELECT visit_id

  FROM Transactions

  GROUP BY visit_id

)

GROUP BY customer_id

### 15) Classes More Than 5 Students

https://leetcode.com/problems/classes-more-than-5-students/


SELECT class

FROM Courses

GROUP BY class

HAVING COUNT(student) >= 5

### 16)  Game Play Analysis I

https://leetcode.com/problems/game-play-analysis-i/

SELECT player_id , MIN(event_date) AS first_login

FROM Activity 

GROUP BY player_id 

### 17) List the Products Ordered in a Period

https://leetcode.com/problems/list-the-products-ordered-in-a-period/

SELECT product_name  , SUM(unit)  AS unit

FROM Products 

RIGHT JOIN Orders 

ON Products.product_id  = Orders.product_id   

WHERE order_date  BETWEEN '2020-02-01' AND '2020-02-29'  

GROUP BY   Products.product_id    

HAVING SUM(unit) >= 100

### 18) Bank Account Summary II

https://leetcode.com/problems/bank-account-summary-ii/

SELECT name as NAME , SUM(amount) AS BALANCE    

FROM USERS

RIGHT JOIN Transactions     

ON Users.account    =   Transactions.account    

GROUP BY Transactions.account

HAVING SUM(amount) > 10000

### 19) Customer Placing the Largest Number of Orders

https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/

SELECT customer_number 

FROM Orders

GROUP BY customer_number    

ORDER BY COUNT(order_number) DESC

LIMIT 1
 
 ### 20) Employees Whose Manager Left the Company

https://leetcode.com/problems/employees-whose-manager-left-the-company/

SELECT employee_id 

FROM Employees  

WHERE salary < 30000 AND manager_id NOT IN
 
 ( 
     SELECT employee_id 

     FROM Employees 

 )

 ORDER BY employee_id
 
 ### 21) Top Travellers

https://leetcode.com/problems/top-travellers/

SELECT name , SUM(IF(distance IS NULL , 0 , distance)) AS travelled_distance 

FROM Users 

LEFT JOIN Rides 

ON Rides.user_id = Users.id  

GROUP BY Rides.user_id

ORDER BY SUM(distance) DESC , NAME ASC

### 22) Capital Gain/Loss

https://leetcode.com/problems/capital-gainloss/

SELECT stock_name , SUM(IF(operation = 'Sell' , price, -price)) AS capital_gain_loss                         # This can be solves using CASE WHEN as well

FROM Stocks 

GROUP BY stock_name    

### 23) Group Sold Products By The Date

https://leetcode.com/problems/group-sold-products-by-the-date/

SELECT sell_date , COUNT(DISTINCT product) AS num_sold , GROUP_CONCAT( DISTINCT product ) AS PRODUCTS

FROM Activities 

GROUP BY sell_date  

ORDER BY sell_date

### 24) Recyclable and Low Fat Products

https://leetcode.com/problems/recyclable-and-low-fat-products/

SELECT product_id

FROM Products

WHERE low_fats = 'Y' AND recyclable = 'Y'

### 25) Percentage of Users Attended a Contest

https://leetcode.com/problems/percentage-of-users-attended-a-contest/

SELECT Register.contest_id , ROUND((COUNT(DISTINCT Register.user_id)) / (COUNT(DISTINCT Users.user_id))*100,2) AS percentage

FROM Users , Register

GROUP BY Register.contest_id

ORDER BY percentage DESC , Register.contest_id ASC

### 26) The Latest Login in 2020

https://leetcode.com/problems/the-latest-login-in-2020/

SELECT user_id , MAX(time_stamp) AS last_stamp          

FROM Logins 

WHERE YEAR(time_stamp) = 2020

GROUP BY user_id 

### 27) Average Time of Process per Machine

https://leetcode.com/problems/average-time-of-process-per-machine/

SELECT machine_id , ROUND((SUM(IF(activity_type = 'end', timestamp, -timestamp))) / COUNT(DISTINCT process_id) , 3) AS processing_time

FROM Activity

GROUP BY machine_id

### 28) Daily Leads and Partners

https://leetcode.com/problems/daily-leads-and-partners/

SELECT date_id , make_name , COUNT(DISTINCT lead_id ) AS unique_leads , COUNT(DISTINCT partner_id) AS unique_partners 

FROM DailySales

GROUP BY date_id , make_name

### 29) Fix Names in a Table

https://leetcode.com/problems/fix-names-in-a-table/

SELECT user_id , CONCAT(UPPER(SUBSTRING(name,1,1)),LOWER(SUBSTRING(name,2))) AS name 

FROM users

ORDER BY user_id ASC

### 30) Count Salary Categories

https://leetcode.com/problems/count-salary-categories/

-- writing alias once in first SELECT statement will suffice

SELECT 'Low Salary' AS category , COUNT(account_id) AS accounts_count FROM accounts where income <20000    

UNION ALL

SELECT 'Average Salary' , COUNT(account_id) AS accounts_count FROM accounts WHERE income BETWEEN 20000 AND 50000

UNION ALL

SELECT 'High Salary' , COUNT(account_id) AS accounts_count FROM accounts WHERE income > 50000

### 31) Department Highest Salary

https://leetcode.com/problems/department-highest-salary/

SELECT d.name AS Department , e.name AS Employee , e.salary AS Salary

FROM Employee e

LEFT JOIN Department d

ON e.DepartmentId = d.Id

WHERE (d.Id, e.Salary) IN (

  SELECT  departmentId , MAX(salary) 

  FROM Employee

  GROUP BY DepartmentId
)

### 32) Game Play Analysis IV

https://leetcode.com/problems/game-play-analysis-iv/

WITH cte_activity AS (

  SELECT * FROM Activity 
)

SELECT ROUND((COUNT(player_id) / (SELECT COUNT(DISTINCT player_id ) FROM cte_activity )),2)  AS fraction

FROM Activity

WHERE DATE_ADD(event_date , INTERVAL 1 DAY) IN (

  SELECT event_date 

  FROM Activity 
)

### 33)  Game Play Analysis IV

https://leetcode.com/problems/game-play-analysis-iv/

SELECT ROUND((SUM(IF(sq.first_login+1 = Activity.event_date , 1 , 0)) / COUNT(DISTINCT Activity.player_id ) ) , 2 ) AS fraction

FROM ( SELECT player_id , min(event_date) AS first_login 

FROM Activity

GROUP BY player_id ) AS sq

JOIN Activity

ON sq.player_id = Activity.player_id

### 34) Sales Analysis III

https://leetcode.com/problems/sales-analysis-iii/

SELECT  DISTINCT s.product_id  , p.product_name

FROM Product p

LEFT JOIN Sales s

ON p.product_id = s.product_id

GROUP BY s.product_id

HAVING MIN(sale_date) >= '2019-01-01' AND MAX(sale_date) <= '2019-03-31'

### 35) Investments in 2016

https://leetcode.com/problems/investments-in-2016/

SELECT ROUND(SUM(i1.tiv_2016),2) AS tiv_2016 

FROM Insurance i1

INNER JOIN Insurance i2

ON i1.pid = i2.pid

WHERE (i1.lat , i1.lon) NOT IN (
  
  SELECT lat , lon 
  FROM Insurance 
  WHERE pid != i2.pid

) 

AND i1.tiv_2015 IN(

  SELECT tiv_2015 
  FROM Insurance 
  WHERE pid != i2.pid
)

### 36) Actors and Directors Who Cooperated At Least Three Times

https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/

SELECT actor_id , director_id

FROM ActorDirector

GROUP BY actor_id , director_id

HAVING COUNT(*) >= 3

### 37) Project Employees I

https://leetcode.com/problems/project-employees-i/

SELECT Project.project_id , ROUND( SUM(experience_years) / COUNT(DISTINCT Employee.employee_id ),2) AS average_years 

FROM Project 

LEFT JOIN Employee

ON Project.employee_id  = Employee.employee_id 

GROUP BY project_id

### 38) Department Top Three Salaries

https://leetcode.com/problems/department-top-three-salaries/

SELECT sq.Department , sq.Employee , sq.salary 

FROM (

SELECT d.name as Department , e.name as Employee, e.Salary as Salary, DENSE_RANK() OVER(PARTITION BY d.name ORDER BY e.Salary DESC) AS r

FROM Employee e

LEFT JOIN Department d

ON e.departmentId = d.id 

ORDER BY Salary DESC 

) AS sq

WHERE r<=3

### 39) Second Highest Salary

https://leetcode.com/problems/second-highest-salary/

SELECT MAX(salary) AS secondHighestSalary

FROM employee

WHERE salary < (SELECT MAX(Salary) FROM Employee) 

### 40) User Activity for the Past 30 Days I

https://leetcode.com/problems/user-activity-for-the-past-30-days-i/

SELECT activity_date AS day , COUNT( DISTINCT user_id) AS active_users 

FROM Activity 

WHERE activity_date BETWEEN DATE_SUB('2019-07-27', INTERVAL 30 DAY)+1 AND '2019-07-27'

GROUP BY activity_date 

### 41) Friend Requests II: Who Has the Most Friends

https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/

WITH cte AS (

  SELECT requester_id, accepter_id
  
  FROM RequestAccepted
  
  UNION ALL
  
  SELECT accepter_id , requester_id
  
  FROM RequestAccepted
  
)

SELECT requester_id AS id, COUNT(accepter_id) AS num

FROM CTE

GROUP BY requester_id

ORDER BY COUNT(accepter_id) DESC

LIMIT 1

### 42) Biggest Single Number

https://leetcode.com/problems/biggest-single-number/submissions/934812702/

SELECT MAX(sq.num) AS num

FROM(

    SELECT num

    FROM MyNumbers 

    GROUP BY num

    HAVING COUNT(num) = 1

) AS sq

### 43) Delete Duplicate Emails

https://leetcode.com/problems/delete-duplicate-emails/description/

DELETE p1 FROM person p1 , person p2

WHERE p1.id > p2.id AND p1.email = p2.email






