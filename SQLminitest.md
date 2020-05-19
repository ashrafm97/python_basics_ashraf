## SQL Mini Test

Question 1:

--    Q1.1

SELECT c.CustomerID, c.CompanyName, c.Country, c.City, c.PostalCode, c.Address
FROM Customers c
WHERE C.City = 'Paris' OR C.City = 'London'


--   Q1.2

SELECT * FROM PRODUCTS
Where QuantityPerUnit LIKE '%bottle%';

--   Q1.3

---We would repeat question above, but add in the Supplier Name and Country.

SELECT * FROM Suppliers

SELECT s.CompanyName, s.Country FROM Products p INNER JOIN suppliers s ON s.SupplierID=p.SupplierID
WHERE QuantityPerUnit LIKE '%bottle%'

--   Q1.4


SELECT COUNT(p.ProductID) AS "Products in categories", c.CategoryName FROM Products p INNER JOIN Categories c ON c.categoryID=p.categoryID
GROUP BY CategoryName
ORDER BY "Products in categories" DESC

--   Q1.5

SELECT CONCAT(e.TitleOfCourtesy,+ ' ' + e.FirstName + ' ' + e.LastName + ', ' + e.City) AS "Employee Details"
From Employees e
ORDER BY "Employee Details"

-- simple concatenation of info, using CONCAT.

-- Q1.7

SELECT o.ShipCountry,
COUNT(Freight) AS "No. of Orders"
FROM Orders o
WHERE Freight > 100
GROUP BY o.ShipCountry
HAVING o.ShipCountry = 'USA' or o.ShipCountry = 'UK'

-- Q1.8

SELECT TOP 1 OrderID,
(UnitPrice * quantity * (1- Discount)) AS "Net Total.",
(UnitPrice * quantity) AS "Gross Total",
(UnitPrice * quantity * (1-discount)) - (UnitPrice * Quantity) AS "Money off"
FROM [Order Details]
ORDER BY 'Money off'

-- Q2

CREATE DATABASE ashraf_db

USE ashraf_db

CREATE TABLE spartans_table
(
    title_of_choice CHAR (2),
    first_name VARCHAR  (10),
    second_name VARCHAR (10),
    university VARCHAR (30),
    course VARCHAR (20),
    Grade DECIMAL (2,1)


)
DROP TABLE spartans_table -- can ease process if undergoing issues...

INSERT INTO spartans_table
VALUES(
    'Mr',
    'Ashraf',
    'Mohamud',
    'City, University of London',
    'Law',
    '2.1'

)

INSERT INTO spartans_table
VALUES(
    'Mr',
    'Delvin',
    'Roy',
    'Bedfordshire',
    'Forensics',
    '2.1'

)

--- you could copy and paste the rest of the class but ....

SELECT * FROM spartans_table

-- to see what you have done...

-- Q3.1

SELECT CONCAT(e.TitleOfCourtesy, + ' ' + e.FirstName + ' ' + e.LastName) AS "Employee Names", e.ReportsTo
from employees e

-- was wrong on this one...

-- Q3.2

SELECT * FROM [Order Details]

SELECT Top 10 DATEDIFF(o.ShippedDate, o.OrderDate) AS "Yearly Customers"
(o.OrderID, o.UnitPrice * o.Quantity AS "Top 10 Customers"
FROM [Order Details] o


-- initially, was confused but was solved....


-- Q3.3

SELECT TOP 10 c.ContactName, ROUND(SUM((unitprice*Quantity*(1-Discount))), 2) AS "Total value of orders"
FROM orders o
INNER JOIN Customers c oN o.CustomerID=c.CustomerID
INNER JOIN [Order Details] od ON o.OrderID=od.OrderID
WHERE o.orderdate BETWEEN '1998-01-01' AND '1998-05-06'
GROUP BY c.ContactName
ORDER BY "Total value of orders" DESC


-- Q3.4
SELECT DISTINCT MONTH(orderdate) AS "Month", AVG(DATEDIFF(d, OrderDate, ShippedDate)) AS "Avg. Ship Time"
FROM Orders
GROUP BY MONTH(OrderDate)
ORDER BY MONTH(OrderDate)

-- needed to add distinct
