# SQL-Project
# 📚 Bookstore SQL Project

A relational database project built around a fictional online bookstore. The dataset covers customers, books, and orders — making it great for practising JOINs, aggregations, subqueries, window functions, and more.

---

## 📁 Dataset Overview

The project uses three tables, each with 500 rows of sample data.

### `Customers`
Stores information about registered customers.

| Column | Type | Description |
|---|---|---|
| `Customer_ID` | INT (PK) | Unique customer identifier |
| `Name` | VARCHAR | Full name |
| `Email` | VARCHAR | Email address |
| `Phone` | BIGINT | Contact number |
| `City` | VARCHAR | City of residence |
| `Country` | VARCHAR | Country of residence |

---

### `Books`
Catalogue of books available in the store.

| Column | Type | Description |
|---|---|---|
| `Book_ID` | INT (PK) | Unique book identifier |
| `Title` | VARCHAR | Book title |
| `Author` | VARCHAR | Author name |
| `Genre` | VARCHAR | Book genre |
| `Published_Year` | INT | Year of publication |
| `Price` | DECIMAL | Price per unit |
| `Stock` | INT | Units currently in stock |

---

### `Orders`
Transactional records linking customers to books.

| Column | Type | Description |
|---|---|---|
| `Order_ID` | INT (PK) | Unique order identifier |
| `Customer_ID` | INT (FK → Customers) | Who placed the order |
| `Book_ID` | INT (FK → Books) | Which book was ordered |
| `Order_Date` | DATE | Date of order (`YYYY-MM-DD`) |
| `Quantity` | INT | Number of copies ordered |
| `Total_Amount` | DECIMAL | Total price paid |

---

## 🔗 Entity Relationship Diagram

```
Customers          Orders              Books
-----------        ---------------     -----------
Customer_ID  ←---  Customer_ID         Book_ID  ---→  Book_ID
Name               Order_ID            Title
Email              Book_ID             Author
Phone              Order_Date          Genre
City               Quantity            Published_Year
Country            Total_Amount        Price
                                       Stock
```

---

## 🗄️ Database Setup

### Import via CSV (MySQL / PostgreSQL / SQLite)

```sql
-- Create tables first, then load data

CREATE TABLE Customers (
    Customer_ID   INT PRIMARY KEY,
    Name          VARCHAR(100),
    Email         VARCHAR(100),
    Phone         BIGINT,
    City          VARCHAR(100),
    Country       VARCHAR(100)
);

CREATE TABLE Books (
    Book_ID        INT PRIMARY KEY,
    Title          VARCHAR(255),
    Author         VARCHAR(100),
    Genre          VARCHAR(50),
    Published_Year INT,
    Price          DECIMAL(6,2),
    Stock          INT
);

CREATE TABLE Orders (
    Order_ID      INT PRIMARY KEY,
    Customer_ID   INT REFERENCES Customers(Customer_ID),
    Book_ID       INT REFERENCES Books(Book_ID),
    Order_Date    DATE,
    Quantity      INT,
    Total_Amount  DECIMAL(8,2)
);
```

---

## 🗒️ Queries

### Basic

| # | Question |
|---|---|
| 1 | Retrieve all books in the "Fiction" genre |
| 2 | Find books published after the year 1950 |
| 3 | List all customers from Canada |
| 4 | Show orders placed in November 2023 |
| 5 | Retrieve the total stock of books available |
| 6 | Find the details of the most expensive book |
| 7 | Show all customers who ordered more than 1 quantity of a book |
| 8 | Retrieve all orders where the total amount exceeds $20 |
| 9 | List all genres available in the Books table |
| 10 | Find the book with the lowest stock |
| 11 | Calculate the total revenue generated from all orders |

### Advanced

| # | Question |
|---|---|
| 1 | Retrieve the total number of books sold for each genre |
| 2 | Find the average price of books in the "Fantasy" genre |
| 3 | List customers who have placed at least 2 orders |
| 4 | Find the most frequently ordered book |
| 5 | Show the top 3 most expensive books in the "Fantasy" genre |
| 6 | Retrieve the total quantity of books sold by each author |
| 7 | List the cities where customers who spent over $30 are located |
| 8 | Find the customer who spent the most on orders |
| 9 | Calculate the stock remaining after fulfilling all orders |

---

## 📂 Project Structure

```
bookstore-sql/
│
├── data/
│   ├── Customers.csv
│   ├── Books.csv
│   └── Orders.csv
│
├── queries/
│   └── bookstore_queries.sql
│
└── README.md
```

---

## 🚀 Getting Started

1. Clone or download this repository
2. Set up your preferred SQL environment (MySQL, PostgreSQL, SQLite, etc.)
3. Run the `CREATE TABLE` statements above
4. Import the CSV files into the corresponding tables
5. Start writing queries!

> **Tip:** Feel free to share the queries you've written — they can be added to the `queries/` folder with comments explaining what each one does.

---

## 📝 Notes

- `Order_Date` is stored as a string in the CSV (`YYYY-MM-DD`). Cast it as `DATE` when creating your table or querying date ranges.
- `Phone` numbers may have leading zeros in some regions — consider storing as `VARCHAR` if precision matters.
- All monetary values use two decimal places.
