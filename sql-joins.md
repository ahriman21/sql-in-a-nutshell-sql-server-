## SQL Joins
A JOIN clause is used to combine rows from two or more tables, based on a related column between them.


#### Types of joins:
- (INNER) JOIN: Returns records that have matching values in both tables

- LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table

- RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table

- FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table


---
> notes: JOIN and INNER JOIN will return the same result.
---

#### Sql commands:

```sql

-- inner join
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers
ON Orders.CustomerID=Customers.CustomerID;


-- left join
-- The LEFT JOIN keyword returns all records from the left table (Customers),
-- even if there are no matches in the right table (Orders).
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;


-- right join
--  returns all records from the right table (Employees), even if there are no matches in the left table (Orders).
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID; 


-- self join
-- A self join is a regular join, but the table is joined with itself.
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;


SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City 
ORDER BY A.City; 
```



