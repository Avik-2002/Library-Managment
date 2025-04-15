# Library-Managment
A library management with MYSQL

# 📚 Library Management Database - MySQL Project

This project demonstrates a simple **library management system** using **MySQL**. It includes table creation, data insertion, and sample queries to manage readers, books, and book issue transactions.

---

## 🏗️ Database Structure

### 1. `readers`
Stores details about library users.

| Column      | Type        | Description              |
|-------------|-------------|--------------------------|
| reader_id   | VARCHAR(6)  | Unique ID for each reader |
| fname       | VARCHAR(30) | First Name                |
| mname       | VARCHAR(30) | Middle Name (nullable)    |
| ltname      | VARCHAR(30) | Last Name                 |
| city        | VARCHAR(15) | City of residence         |
| mobile      | VARCHAR(10) | Contact number            |
| occupation  | VARCHAR(10) | Job/Role of the reader    |
| dob         | DATE        | Date of birth             |

---

### 2. `Book`
Stores the details of books available in the library.

| Column    | Type         | Description               |
|-----------|--------------|---------------------------|
| bid       | VARCHAR(5)   | Unique book ID            |
| bname     | VARCHAR(40)  | Book name                 |
| bdomain   | VARCHAR(30)  | Category/Domain of book   |

---

### 3. `active_readers`
Stores info about accounts holding books currently or previously.

| Column      | Type         | Description                              |
|-------------|--------------|------------------------------------------|
| account_id  | VARCHAR(6)   | Unique account ID                        |
| reader_id   | VARCHAR(6)   | Foreign key linked to `readers` table   |
| bid         | VARCHAR(6)   | Foreign key linked to `Book` table      |
| atype       | VARCHAR(10)  | Account type (`Premium` or `Regular`)   |
| astatus     | VARCHAR(10)  | Account status (`Active`, `Terminated`, `Suspended`) |

---

### 4. `bookissue_details`
Logs each book issued using an account.

| Column                  | Type         | Description                              |
|-------------------------|--------------|------------------------------------------|
| issuenumber             | VARCHAR(6)   | Unique issue transaction number         |
| account_id              | VARCHAR(6)   | Foreign key to `active_readers`         |
| bid                     | VARCHAR(20)  | Book ID                                  |
| bookname                | VARCHAR(50)  | Name of the book                         |
| numbers_of_book_issued  | INT(7)       | Number of copies issued                  |

---

## 📌 Sample Queries

```sql
-- View all readers
SELECT * FROM readers;

-- List all books
SELECT * FROM Book;

-- Show all active accounts
SELECT * FROM active_readers WHERE astatus = 'Active';

-- Show all terminated accounts
SELECT * FROM active_readers WHERE astatus = 'Terminated';

-- Count total Premium accounts
SELECT COUNT(account_id) FROM active_readers WHERE atype = 'Premium';

-- View all book issue transactions
SELECT * FROM bookissue_details;
