
## SQL Server Query Test:

- Show the Top 2 products for each category
- Product that generated the most revenue per customer
- Total revenue per customer
- First date where total revenue per customer exceeds 5000
- Month with the highest total sales
- Customers with no purchases
- Top-selling product overall
- Percentage of sales by category
- Customer ranking by spending
- Pivot sales by category
- Detect multiple sales per customer on the same day
- Least-selling product by category
- Customers who purchased in all categories
- Average ticket per customer
- Day with the highest revenue
- Detect products that have never been sold
- Product with the greatest contribution to the overall total

## Database Structure Script:

```
CREATE TABLE Clients (
ClientId INT PRIMARY KEY,
Name VARCHAR(100),
RegistrationDate DATE
);

CREATE TABLE Categories (
CategoryId INT PRIMARY KEY,
Name VARCHAR(100)
);

CREATE TABLE Products ( 
ProductId INT PRIMARY KEY, 
Name VARCHAR(100), 
CategoryId INT, 
DECIMAL Price(10.2), 
FOREIGN KEY (CategoriaId) REFERENCES Categories(CategoriaId)
);

CREATE TABLE Sales ( 
SaleId INT PRIMARY KEY, 
ClientId INT, 
ProductId INT, 
Date DATE, 
INT quantity, 
FOREIGN KEY (CustomerId) REFERENCES Customers(CustomerId), 
FOREIGN KEY (ProductId) REFERENCES Products(ProductId)
);

-- Insert data
INSERT INTO Customers VALUES
(1,'Ana','2024-01-10'),
(2,'Luis','2024-02-15'),
(3,'Carla','2024-03-01');

INSERT INTO Categories VALUES
(1,'Electronics'),
(2,'Clothing'),
(3,'Home');

INSERT INTO Products VALUES
(1,'Laptop',1,3500),
(2,'Mouse',1,50),
(3,'Shirt',2,80),
(4,'Chair',3,300),
(5,'Keyboard',1,120);

INSERT INTO Sales VALUES
(1,1,1,'2025-01-01',1),
(2,1,2,'2025-01-02',2),
(3,1,5,'2025-01-05',1),
(4,2,3,'2025-01-03',3),
(5,2,1,'2025-01-10',1),
(6,3,4,'2025-01-02',2),
(7,3,2,'2025-01-04',5),
(8,1,3,'2025-01-15',4),
(9,2,2,'2025-01-20',10),
(10,3,1,'2025-01-25',1);

```

## Form with these fields that allows adding:

a) Client (Request)
b) Product (Request)
c) Category (Autofill)
d) Price (Autofill)
e) Quantity (Request)
f) Add button

## And a simple table containing these columns:

a) Date
b) Client
c) Product
d) Category
e) Quantity
f) Total

## This must be done in two projects:

1. **Backend:** Generate an API with two methods to add and list sales.

2. **Frontend:** Only HTML and JavaScript to generate the form and table, and consume the services using JavaScript's fetch method.