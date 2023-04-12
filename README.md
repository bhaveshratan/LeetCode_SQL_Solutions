# LeetCode_SQL_Solutions
Solutions to SQL problems on LeetCode

1) Customers Who Never Order

https://leetcode.com/problems/customers-who-never-order/


select name as Customers

from customers

left join orders

on Customers.id = Orders.customerId

where customerId IS NULL;

2) Combine Two Tables

https://leetcode.com/problems/combine-two-tables/


SELECT firstName , lastName , city , state

FROM Person

LEFT JOIN Address

ON Person.personId = Address.personId;

3) Number of Unique Subjects Taught by Each Teacher

https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/


SELECT teacher_id , COUNT( DISTINCT subject_id ) as cnt

FROM Teacher

GROUP BY teacher_id;

4) Rising Temperature

https://leetcode.com/problems/rising-temperature/

SELECT Weath1.id 

FROM Weather Weath1, Weather Weath2

WHERE dateDiff(Weath1.recordDate, Weath2.recordDate) = 1 AND Weath1.temperature  > Weath2.temperature

5) Big Countries

https://leetcode.com/problems/big-countries/

SELECT name, population , area    

FROM World 

WHERE area >= 3000000 OR population >= 25000000


6) Duplicate Emails

https://leetcode.com/problems/duplicate-emails/

SELECT email as Email

FROM Person 

GROUP BY email

HAVING COUNT(email) > 1

7) Sales Person

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

8) Find Customer Referee

https://leetcode.com/problems/find-customer-referee/

SELECT name 

FROM Customer

WHERE referee_id IS NULL OR referee_id !=2

9) Find Followers Count

https://leetcode.com/problems/find-followers-count/

SELECT user_id , COUNT(follower_id) as followers_count

FROM Followers 

GROUP BY user_id 

ORDER BY user_id 

10) Triangle Judgement

https://leetcode.com/problems/triangle-judgement/

SELECT x,y,z,

CASE 

  WHEN (x+y > z AND y+z > x AND x+z > y) THEN 'Yes'ELSE 'No'

END AS triangle

FROM Triangle;

11) Employee Bonus

https://leetcode.com/problems/employee-bonus/

SELECT name , bonus 

FROM Employee

LEFT JOIN Bonus

ON Employee.empId = Bonus.empId 

WHERE bonus < 1000 OR bonus IS NULL

12) Employees Earning More Than Their Managers

https://leetcode.com/problems/employees-earning-more-than-their-managers/

SELECT e1.name  AS Employee 

FROM Employee  e1

LEFT JOIN Employee e2

ON e1.managerId = e2.id 

WHERE e1.salary > e2.salary


13) Patients With a Condition

https://leetcode.com/problems/patients-with-a-condition/

SELECT * 

FROM Patients

WHERE conditions  LIKE 'DIAB1%' OR conditions  LIKE '% DIAB1%'                     # Note the space before DIAB1

14) Customer Who Visited but Did Not Make Any Transactions

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

15) Classes More Than 5 Students

https://leetcode.com/problems/classes-more-than-5-students/


SELECT class

FROM Courses

GROUP BY class

HAVING COUNT(student) >= 5

16)  Game Play Analysis I

https://leetcode.com/problems/game-play-analysis-i/

SELECT player_id , MIN(event_date) AS first_login

FROM Activity 

GROUP BY player_id 

17) List the Products Ordered in a Period

https://leetcode.com/problems/list-the-products-ordered-in-a-period/

SELECT product_name  , SUM(unit)  AS unit

FROM Products 

RIGHT JOIN Orders 

ON Products.product_id  = Orders.product_id   

WHERE order_date  BETWEEN '2020-02-01' AND '2020-02-29'  

GROUP BY   Products.product_id    

HAVING SUM(unit) >= 100

18) Bank Account Summary II

https://leetcode.com/problems/bank-account-summary-ii/

SELECT name as NAME , SUM(amount) AS BALANCE    

FROM USERS

RIGHT JOIN Transactions     

ON Users.account    =   Transactions.account    

GROUP BY Transactions.account

HAVING SUM(amount) > 10000

19) Customer Placing the Largest Number of Orders

https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/

SELECT customer_number 

FROM Orders

GROUP BY customer_number    

ORDER BY COUNT(order_number) DESC

LIMIT 1
 











