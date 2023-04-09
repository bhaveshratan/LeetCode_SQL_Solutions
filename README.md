# LeetCode_SQL_Solutions
Solutions to SQL problems on LeetCode

1) Customers Who Never Order

https://leetcode.com/problems/customers-who-never-order/


select name as Customers

from customers

left join orders

on Customers.id = Orders.customerId

where customerId IS NULL

2) Combine Two Tables

https://leetcode.com/problems/combine-two-tables/


SELECT firstName , lastName , city , state

FROM Person

LEFT JOIN Address

ON Person.personId = Address.personId

3)
