## basic sql commands in a nutshell:

#### select queries:
- ` SELECT DISTINCT Country FROM Customers; `


- ` SELECT COUNT(DISTINCT Country) FROM Customers; `


- ` SELECT * FROM Customers WHERE CustomerID=1; `


- ` SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC; `


- ` SELECT * FROM Customers WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%'); `


- ' SELECT * FROM Customers WHERE CustomerID NOT BETWEEN 10 AND 60; '


- ` SELECT * FROM Customers WHERE City IN ('Paris', 'London'); `


- ` SELECT column_names FROM table_name WHERE column_name IS NULL; `

- ` SELECT TOP number column_name(s) FROM table_name WHERE condition; `



#### Insert data queries:
```sql

INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...); 

```



#### Update data queries:
```sql

UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition; 

```



#### SQL DELETE Statement:
```sql

DELETE FROM table_name WHERE condition;

```


#### SQL Aggregate Functions:
An aggregate function is a function that performs a calculation on a set of values, and returns a single value.

Aggregate functions are often used with the GROUP BY clause of the SELECT statement. The GROUP BY clause splits the result-set into groups of values and the aggregate function can be used to return a single value for each group.

```sql

-- select the prodcut from Products that has the least price:
SELECT MIN(Price)
FROM Products;


-- select cheapest product group by (base on each) category:
SELECT MIN(Price) AS SmallestPrice, CategoryID
FROM Products
GROUP BY CategoryID;


-- Find the number of products where Price is higher than 20:
SELECT COUNT(ProductID)
FROM Products
WHERE Price > 20;

```


#### The SQL LIKE Operator
The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.

There are two wildcards often used in conjunction with the LIKE operator:

    - The percent sign % represents zero, one, or multiple characters
    - The underscore sign _ represents one, single character


```sql

-- customerNames that start with 'a'
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%'; 


-- Return all customers from a city that starts with 'L' followed by one wildcard character, then 'nd' and then two wildcard characters:
SELECT * FROM Customers
WHERE city LIKE 'L_nd__'; 


-- Return all customers from a city that contains the letter 'L':
SELECT * FROM Customers
WHERE city LIKE '%L%'; 


```



#### Union:
The UNION operator is used to combine the result-set of two or more SELECT statements.

- Every SELECT statement within UNION must have the same number of columns
- Every SELECT statement within UNION must have the same number of columns
- The columns in every SELECT statement must also be in the same order

> note: usually it is used when two tables have similar column (names).

```sql

SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2; 

```


#### Having:
The HAVING clause was added to SQL because you cannot use WHERE on aggregate fuctions:

```sql

-- example 1
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;



-- example 2
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;

```



