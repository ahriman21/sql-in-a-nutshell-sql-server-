## intermediary & advanced Sql commands:
this section provides exists, any, all, select into, functions, views, triggers, SP, json


#### functions:
you can write your own functios and call them whenever you want.

```sql

CREATE FUNCTION func_name (@param1 int, @param2 char(30))
returns float   		-- specify the return type
as begin			-- begin the body of function
	declare @result float;  -- declare a variable
	select @result = score from students where studentCode = @param2;
	return @result;

end;


```



#### views:
In SQL, a view is a virtual table based on the result-set of an SQL statement.

A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database.

> Note: A view always shows up-to-date data! The database engine recreates the view, every time a user queries it.

```sql

-- how to create a view:
CREATE VIEW view_name
AS
SELECT column1, column2, ...
FROM table_name
WHERE condition; 


-- example of creating a view
CREATE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil'; 


-- example of calling a view:
 SELECT * FROM [Brazil Customers]; 


-- updating a view
CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;


-- dropping a view
DROP VIEW view_name;
```




#### triggers:
 A trigger is a special type of stored procedure that automatically runs when an event occurs in the database server. DML triggers run when a user tries to modify data through a data manipulation language (DML) event. DML events are INSERT, UPDATE, or DELETE statements on a table or view. These triggers fire when any valid event fires, whether table rows are affected or not. For more information, see DML Triggers.

DDL triggers run in response to a variety of data definition language (DDL) events. These events primarily correspond to Transact-SQL CREATE, ALTER, and DROP statements, and certain system stored procedures that perform DDL-like operations.

Logon triggers fire in response to the LOGON event that's raised when a user's session is being established. 

###### what are INSTEAD OF, FOR, AFTER:
> INSTEAD OF: Specifies that the DML trigger launches instead of the triggering SQL statement.

> FOR, AFTER: FOR or AFTER specifies that the DML trigger fires only when all operations specified in the triggering SQL statement have launched successfully

```sql

-- syntax
CREATE TRIGGER trigger_name
ON {table | view}
{ for | after | instead of }
{INSERT | UPDATE | DELETE}
AS
{sql_statement}


-- example
CREATE TRIGGER production.trg_product_audit 	-- name
ON production.products 				-- specifying target table 
AFTER INSERT, DELETE				-- specifying operation		
AS BEGIN					-- trigger body begins

	PRINT 'First message'			-- what happens when sql is triggered


END						-- end of body



```



#### exists, any, all:




#### SP (stored procedures):
A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.

So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it.

```sql


-- create a simple SP:
CREATE PROCEDURE SelectAllCustomers
AS
SELECT * FROM Customers
GO;

-- call a SP:
EXEC SelectAllCustomers;


-- createa SP with parameters:
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
AS
SELECT * FROM Customers WHERE City = @City
GO;

-- call a SP with parameters:
EXEC SelectAllCustomers @City = 'London'; 
```



#### indexing:
The CREATE INDEX statement is used to create indexes in tables.

Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.

Note: Updating a table with indexes takes more time than updating a table without (because the indexes also need an update). So, only create indexes on columns that will be frequently searched against.


```sql

CREATE INDEX index_name
ON table_name (column1, column2, ...); 

```



#### JSON
JSON is a popular textual data format that's used for exchanging data in modern web and mobile applications. JSON is also used for storing unstructured data in log files or NoSQL databases

```json
{
  [
    {
        "name": "John",
        "skills": [ "SQL", "C#", "Azure" ]
    },
    {
        "name": "Jane",
        "surname": "Doe"
    }
  ]
}

```

* you can write a json format data in a variable in sql and retrieve it:
```sql

-- write a json data in a variable:
declare @data nvarchar(400) = 
N'{

	"name": "bob",
	"age" : "19",

}';


-- read from a json variable:
select json_vlaue(@data, "$.name") as name;


```





* map json in sql tables:
```sql

-- our json data example:
declare @data nvarchar(max);
set @data = N'{

    "customers":
                ] 
		   {
			"name": "bob",
			"email": "bob@bob.com",
			"addresses": ["address1", "address2"],
		   },
		   {
			"name": "alice",
			"email": "alice@asd.com",
			...
		   },

                ]  

}'


-- mapping json to sql tables:
select * from openjson(@data, '$.customers')
with (
    name nvarchar(40) '$.name',
    email varchar(40) '$.email'
    addresses 
),



-- map a sql table into json (convert table to json):
 
```




* insert json in sql tables:
```sql

CREATE TABLE products (
    id INT PRIMARY KEY IDENTITY,
    details NVARCHAR(MAX) CHECK (ISJSON(details) = 1)
);

INSERT INTO products (details) VALUES
('{"name": "Laptop", "price": 1200, "features": ["16GB RAM", "1TB SSD"]}');

SELECT JSON_VALUE(details, '$.name') FROM products WHERE JSON_VALUE(details, '$.price') > 1000;

```





* export json from a table:
```sql

-- Export to JSON using FOR JSON PATH
SELECT ProductID, ProductName, Price
FROM Products
FOR JSON PATH;

-- Output:
-- [{"ProductID":1,"ProductName":"Laptop","Price":1200.00},{"ProductID":2,"ProductName":"Mouse","Price":25.00},{"ProductID":3,"ProductName":"Keyboard","Price":75.00}]


-- Export with a root element
SELECT ProductID, ProductName, Price
FROM Products
FOR JSON PATH, ROOT('products');

-- Output:
-- {"products":[{"ProductID":1,"ProductName":"Laptop","Price":1200.00},{"ProductID":2,"ProductName":"Mouse","Price":25.00},{"ProductID":3,"ProductName":"Keyboard","Price":75.00}]}


```



* import json data into a sql table:
```sql

-- Sample JSON data
DECLARE @json NVARCHAR(MAX) = N'[
    {"ProductID": 1, "ProductName": "Laptop", "Price": 1200},
    {"ProductID": 2, "ProductName": "Mouse", "Price": 25},
    {"ProductID": 3, "ProductName": "Keyboard", "Price": 75}
]';

-- Create a sample table (if it doesn't exist)
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(50),
    Price DECIMAL(10, 2)
);

-- Insert data from JSON
INSERT INTO Products (ProductID, ProductName, Price)
SELECT ProductID, ProductName, Price
FROM OPENJSON (@json)
WITH (
    ProductID INT '$.ProductID',
    ProductName VARCHAR(50) '$.ProductName',
    Price DECIMAL(10, 2) '$.Price'
);

```



* read json from a json file and insert into a sql table:
```sql


-- Read JSON from file and insert into the table
INSERT INTO Products (ProductID, ProductName, Price)
SELECT ProductID, ProductName, Price
FROM OPENROWSET (BULK 'C:\path\to\your\data.json', SINGLE_CLOB) AS json_data
CROSS APPLY OPENJSON(json_data.BulkColumn)
WITH (
    ProductID INT '$.ProductID',
    ProductName VARCHAR(255) '$.ProductName',
    Price DECIMAL(10, 2) '$.Price'
);

```
