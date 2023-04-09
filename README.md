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
