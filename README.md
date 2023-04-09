# LeetCode_SQL_Solutions
Solutions to SQL problems on LeetCode

1) Customers Who Never Order

https://leetcode.com/problems/customers-who-never-order/


select name as Customers

 from customers

 left join orders

    on Customers.id = Orders.customerId

where customerId IS NULL
