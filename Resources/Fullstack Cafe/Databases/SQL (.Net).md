# Entry

## Q1: Define a Temp Table

A Temp Table (Temporary Table) is a short-lived table used to store intermediate results or perform complex operations in SQL, especially within sessions or procedures. Temp tables exist temporarily during the connection/session and are automatically dropped when the session ends or explicitly dropped. In SQL Server, they start with a `#` (local temp table, visible only in the current session) or `##` (global temp table, visible to all sessions). Temp tables are useful for breaking down large queries, storing staging data, or handling complex manipulations that may be tricky in a single query. They behave much like regular tables, supporting indexes and constraints.

```sql
-- Create and use a temp table in SQL Server
CREATE TABLE #CustomerTemp (CustomerId INT, Name NVARCHAR(100));
INSERT INTO #CustomerTemp VALUES (1, 'Alice'), (2, 'Bob');
SELECT * FROM #CustomerTemp;
DROP TABLE #CustomerTemp;
```
---

## Q2: What is "PRIMARY KEY"?

A PRIMARY KEY is a constraint in SQL used to uniquely identify each row in a table. It enforces uniqueness (no duplicate values) and ensures that the column(s) defining the primary key cannot contain NULL values. Each table can have only one primary key, which may consist of one or multiple columns (composite key). The primary key is often used to reference records in other tables via foreign keys and improves data integrity and retrieval speed.

```sql
-- Defining a primary key on a table
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name NVARCHAR(100)
);
```
---

## Q3: What is a "VIEW"?

A VIEW is a virtual table representing the result of a saved SQL SELECT query. It does not store data physically but provides a way to present, filter, or join data from one or more tables. Views can simplify complex queries, provide abstraction, and restrict access to data (showing only selected columns or rows). You can query a view just as you would a table, but cannot always perform updates directly through a view.

```sql
-- Creating and selecting from a view
CREATE VIEW ActiveEmployees AS
SELECT EmployeeID, Name FROM Employees WHERE IsActive = 1;
SELECT * FROM ActiveEmployees;
```
---

# Junior

## Q4: What is Normalisation?

Normalization is the process of organizing data in a database to minimize redundancy and dependency. Its main goal is to break down tables into smaller, related tables with clear relationships to ensure data integrity and efficient storage. Normalization involves applying a series of "normal forms": 1NF (no repeating groups), 2NF (no partial dependencies on primary keys), 3NF (no transitive dependencies), and so on. Proper normalization leads to clearer data structures, simplifies updates, and avoids anomalies.

```sql
-- Example 1NF: Split repeating groups into separate rows
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE
);
```
---

## Q5: What is the difference between Data Definition Language (DDL) and Data Manipulation Language (DML)?

DDL commands define or alter the structure of database objects such as tables, schemas, and indexes. Examples include CREATE, ALTER, and DROP. DML commands, on the other hand, deal with the manipulation of data within objects—commands like SELECT, INSERT, UPDATE, and DELETE. DDL changes the schema and may cause implicit commits, while DML works on table data and can be rolled back.

```sql
-- DDL example
CREATE TABLE Departments (DepartmentID INT, DepartmentName NVARCHAR(100));

-- DML example
INSERT INTO Departments VALUES (1, 'Sales');
SELECT * FROM Departments;
```
---

## Q6: What is the difference between "TRUNCATE" and "DELETE"?

Both commands remove data from tables, but TRUNCATE is more efficient; it deletes all rows without logging individual row deletions or firing triggers, and typically resets identity columns. DELETE is row-based, can filter with WHERE, logs each row, and can activate triggers. DELETE operations can be rolled back if within a transaction, while TRUNCATE, although transactional in SQL Server, cannot target specific rows or tables with foreign key constraints.

```sql
-- Example
DELETE FROM Customers WHERE Country = 'USA';
TRUNCATE TABLE Customers; -- Deletes all rows
```
---

## Q7: What is "DEFAULT"?

DEFAULT is a constraint set on a column that assigns a value automatically when no explicit value is supplied on INSERT. It's useful to ensure columns always have a value, even if the user does not provide one.

```sql
-- Example with DEFAULT constraint
CREATE TABLE Products (
    ProductID INT,
    Available BIT DEFAULT 1
);
INSERT INTO Products (ProductID) VALUES (1001); -- Available will be 1
```
---

## Q8: What is "FOREIGN KEY"?

A FOREIGN KEY enforces a link between data in two tables, maintaining referential integrity. It requires that values in a column or set of columns match values in the primary key of another table. This ensures that no orphan records can exist—every value in the foreign key must correspond to an existing primary key.

```sql
-- Foreign key example
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```
---

## Q9: What is the difference between "INNER JOIN", "OUTER JOIN", "FULL OUTER JOIN"?

INNER JOIN returns only rows with matching values in both tables. OUTER JOIN (LEFT or RIGHT) returns matched rows plus all rows from one table, with NULLs where missing matches occur. FULL OUTER JOIN combines the results of both LEFT and RIGHT joins, returning all records from both tables with NULLs where no match exists.

```sql
-- INNER JOIN
SELECT * FROM A INNER JOIN B ON A.ID = B.ID;
-- LEFT OUTER JOIN
SELECT * FROM A LEFT OUTER JOIN B ON A.ID = B.ID;
-- FULL OUTER JOIN
SELECT * FROM A FULL OUTER JOIN B ON A.ID = B.ID;
```
---

## Q10: What is the difference between "UNION" and "UNION ALL"?

UNION combines results from two or more SELECT queries, eliminating duplicate rows. UNION ALL does the same but includes all duplicates. UNION is slower due to the duplicate-checking process. Both require the same number and type of columns.

```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers;

SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers;
```
---

## Q11: Describe the difference between "truncate" and "delete".

TRUNCATE removes all rows from a table quickly, without logging each deletion and usually without activating triggers. It resets identity columns and does not allow WHERE filters. DELETE removes rows one at a time, can filter which rows to remove, logs each action, and can fire triggers. DELETE is suitable for selective removal; TRUNCATE for wiping out whole tables.

```sql
DELETE FROM Employees WHERE IsRetired = 1;
TRUNCATE TABLE Employees; -- Removes all rows
```
---

## Q12: What is Denormalization?

Denormalization involves intentionally introducing redundancy by merging tables or adding duplicates, aimed at improving query performance or simplifying queries. It’s often used in reporting or analytical databases, where faster reads are prioritized over update efficiency. Although it increases storage use and risks of data anomalies, it can significantly speed up complex queries that require joins or aggregations across many tables.

```sql
-- Example: combining customer and order info in one table for reporting
CREATE TABLE OrderSummary (
    OrderID INT,
    CustomerName NVARCHAR(100),
    OrderTotal MONEY
);
```
---

# Mid

## Q13: What's the difference between a Primary Key and a Unique Key?

Both PRIMARY KEY and UNIQUE KEY constraints enforce uniqueness of column values; however, a table can only have one PRIMARY KEY, which cannot have NULLs, while it can have multiple UNIQUE KEYS, which can accept one or more NULLs (depending on database). PRIMARY KEY is mainly used for table identification and relationships (foreign keys), while UNIQUE KEY is used for enforcing alternate candidate keys.

```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    Email NVARCHAR(100) UNIQUE
);
```
---

## Q14: What are the differences between Clustered and a Non-clustered index?

A Clustered Index dictates the physical order of rows in the table (a table can have only one). The table data is the index. Non-clustered Indexes create a separate structure holding pointers to the actual table data; you can have many non-clustered indexes per table. Clustered indexes are faster for range queries and sorting on the key column, while non-clustered indexes offer flexible access paths for frequent searches not covered by the clustered index.

```sql
-- Clustered index (usually PRIMARY KEY)
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,  -- Clustered by default
    OrderDate DATE
);

-- Non-clustered index
CREATE NONCLUSTERED INDEX idx_OrderDate ON Orders(OrderDate);
```
---

## Q15: How does a Hash index work?

A hash index uses a hash function to map search keys to locations (buckets) in the index. The hash function computes a "hash code" for the search key, which is then used as an address to find the data. This allows extremely fast lookup for equality searches. However, range queries or ordering are inefficient, since the structure does not preserve order.

```sql
-- Syntax for HASH index (SQL Server In-Memory OLTP example)
CREATE TABLE Accounts (
    AccountID INT PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 1000),
    Balance MONEY
);
```
---

## Q16: How a database index can help performance?

Indexes allow faster data retrieval by maintaining sorted or hashed copies of key search columns, so the database engine avoids scanning the entire table for each query. When queries include WHERE clauses, JOINs, or ORDER BY on indexed columns, the index is scanned to quickly locate matching rows. Indexes are especially effective for read-heavy workloads, though they add overhead during data modification operations.

```sql
-- Create index to speed up lookups by Email
CREATE INDEX idx_Email ON Users (Email);
```
---

## Q17: What is the difference between "WHERE" clause and "HAVING" clause?

WHERE filters rows before grouping or aggregations occur, so it operates on raw table data. HAVING filters after grouping, so it applies conditions to grouped/aggregated results. You use WHERE for column values, and HAVING for aggregate functions or post-aggregation conditions.

```sql
-- WHERE filters rows before GROUP BY
SELECT * FROM Orders WHERE OrderTotal > 100;

-- HAVING filters groups after GROUP BY
SELECT CustomerID, SUM(OrderTotal) AS Total
FROM Orders
GROUP BY CustomerID
HAVING SUM(OrderTotal) > 500;
```
---

## Q18: What is the difference between "JOIN" and "UNION"?

JOIN is used to combine columns from multiple tables based on related columns (typically using keys), returning a wider result set with columns from each table. UNION combines the result sets of 2+ SELECT queries into a single set, stacking rows on top of each other, requiring the same number and types of columns.

```sql
-- JOIN example
SELECT A.ID, B.Name FROM TableA A JOIN TableB B ON A.ID = B.AID;

-- UNION example
SELECT Name FROM Employees
UNION
SELECT Name FROM Customers;
```
---

## Q19: What is Collation?

Collation defines the set of rules for how data is sorted and compared in SQL—covering aspects like case-sensitivity, accent-sensitivity, and language. Each database, table, or column can have its own collation, affecting sorting and filtering behavior. Collation mismatches can result in errors or unexpected query results, especially when joining tables with different collations.

```sql
-- Create a table with specific collation
CREATE TABLE Customers (
    Name NVARCHAR(100) COLLATE Latin1_General_CS_AS
);
```
---

## Q20: What is the difference between "INNER JOIN" and "OUTER JOIN"?

INNER JOIN returns only those rows where the join condition matches in both tables. OUTER JOINs include records that have no match in one table: LEFT OUTER JOIN adds all rows from the left table (plus matches from the right), RIGHT OUTER JOIN does the reverse, and FULL OUTER JOIN includes rows from both tables even when there’s no match, filling in NULLs where data is missing.

```sql
-- INNER JOIN
SELECT * FROM Orders o INNER JOIN Customers c ON o.CustomerID = c.CustomerID;
-- LEFT OUTER JOIN
SELECT * FROM Orders o LEFT OUTER JOIN Customers c ON o.CustomerID = c.CustomerID;
```
---

## Q21: How can "VIEW" be used to provide security layer for your app?

A VIEW in SQL serves as a virtual table representing the result of a predefined query. Views can be leveraged as a security mechanism to restrict access to sensitive data by exposing only necessary columns and rows to application users. Instead of granting direct access to base tables, permissions can be set such that users or applications have access only to views. Through this, you can hide confidential columns, apply row-level security (using WHERE clauses), and limit data modification possibilities. Views can enforce business rules, mask sensitive information, and restrict SELECT, INSERT, UPDATE, or DELETE permissions to user-defined subsets. For example, an employee might see only their own records via a view even though the base table contains all employees’ data. In enterprise environments, complex logic can be encapsulated in views to control exactly what’s exposed.

```sql
-- Create a view that only exposes non-sensitive columns from the Employees table
CREATE VIEW EmployeePublicView AS
SELECT EmployeeID, Name, Department
FROM Employees
WHERE IsActive = 1;

-- Grant access to the view, not the base table
GRANT SELECT ON EmployeePublicView TO AppUser;
```

---

## Q22: Discuss "INNER JOIN" on vs "WHERE" clause (with multiple "FROM" tables)

Using "INNER JOIN ... ON" syntax is the ANSI-standard and preferred way to perform joins in SQL, clearly expressing join conditions separate from filter conditions. Using the "WHERE" clause to join tables (by listing multiple tables in the "FROM" and specifying join conditions in "WHERE") is the older syntax. Both ultimately produce the same execution plan but separating join conditions (in "ON") from filters (in "WHERE") improves readability and maintainability. In complex queries or with OUTER JOINs, using "JOIN ... ON" avoids ambiguity and accidental cross joins. The join conditions in "ON" are evaluated first, forming the rowset, which is then filtered by "WHERE." Some SQL features can only be expressed with explicit JOIN syntax, like OUTER JOINs.

```sql
-- ANSI-standard (preferred)
SELECT a.Name, b.OrderID
FROM Customers a
INNER JOIN Orders b ON a.CustomerID = b.CustomerID
WHERE a.Country = 'USA';

-- Old style (non-recommended)
SELECT a.Name, b.OrderID
FROM Customers a, Orders b
WHERE a.CustomerID = b.CustomerID AND a.Country = 'USA';
```

---

## Q23: Define ACID Properties

ACID stands for Atomicity, Consistency, Isolation, and Durability—fundamental properties that ensure reliable database transactions. Atomicity ensures transactions are fully completed or not executed at all. Consistency guarantees that a transaction transforms the database from one valid state to another, maintaining all rules and constraints. Isolation ensures that concurrent transactions do not affect each other's execution; their intermediate states remain invisible to one another. Durability means that once a transaction is committed, its results are permanent, even in the event of a system failure. These properties collectively maintain data integrity and reliability, supporting robust application behaviors in multi-user environments.

```sql
-- Example: All steps are atomic; on error, changes are rolled back
BEGIN TRAN;
  UPDATE BankAccounts SET Balance = Balance - 100 WHERE AccountID = 1;
  UPDATE BankAccounts SET Balance = Balance + 100 WHERE AccountID = 2;
COMMIT;
```

---

## Q24: What’s the difference between Azure SQL Database and Azure SQL Managed Instance?

Azure SQL Database is a fully managed, single database service optimized for modern cloud applications; it abstracts away hardware, OS, and most maintenance tasks, exposing only the SQL engine and database. It offers high availability, backups, and scaling but doesn’t support all SQL Server features (e.g., some agent jobs, cross-database queries). Azure SQL Managed Instance (MI) is closer to a managed SQL Server instance; it preserves full engine compatibility, makes migration easier, and supports features like cross-database queries, SQL Agent, and more. MI targets organizations needing near on-premises SQL Server parity but without infrastructure management. Connectivity, VNET support, and pricing models also differ, with MI generally having more control and complexity than SQL Database.

```sql
-- Azure SQL Database: For cloud-native, serverless, per-database billing.
-- Azure Managed Instance: For near-lift-and-shift migrations, instance-wide features.
```

---

## Q25: What is the cost of having a database index?

While indexes can greatly improve query performance, they incur costs. Indexes consume additional storage space proportional to the size and number of indexed columns and rows. Each DML operation (INSERT, UPDATE, DELETE) on the underlying table may require corresponding updates to all relevant indexes, causing extra processing overhead and possibly slowing write-intensive workloads. Index maintenance (like rebuilds or defragmentation) also adds to administrative costs. Excessive or inappropriate indexes may degrade performance rather than help it. Choosing which indexes to create requires balancing read performance needs with these space and maintenance costs.

```sql
-- Adding an index takes storage and affects DML operations
CREATE INDEX idx_lastname ON Employees(LastName);
```

---

## Q26: What is faster, one big query or many small queries?

In most cases, a single well-optimized query is faster than multiple small queries performing equivalent work. A single query allows the SQL optimizer to generate an efficient execution plan and minimize repeated I/O, network round-trips, and context switches. Multiple queries can increase network latency, risk inconsistent reads, and are harder to optimize globally. However, if the one "big" query is overly complex or unoptimized, small tailored queries may outperform it. Batch operations (set-based logic) are preferable to row-by-row actions (RBAR). Still, specific scenarios, such as extremely complex joins or when processing different partitions, may warrant splitting work.

```sql
-- One big query (preferred for set logic)
SELECT Name, Salary FROM Employees WHERE Department = 'IT';

-- Many small queries (not preferred except for very specific cases)
SELECT Name, Salary FROM Employees WHERE Department = 'IT' AND EmployeeID = 1;
SELECT Name, Salary FROM Employees WHERE Department = 'IT' AND EmployeeID = 2;
```
---

# Senior

## Q27: What is the difference among "UNION", "MINUS" and "INTERSECT"?

"UNION" combines results of two queries and returns distinct rows present in either, removing duplicates. "MINUS" (or "EXCEPT" in SQL Server) returns rows from the first query not present in the second. "INTERSECT" returns only rows present in both queries. These set operators allow comparison and combination of different result sets. All require the same number and type of columns in both queries. UNION’s uniqueness property can be expensive for large datasets, while "UNION ALL" returns duplicates.

```sql
SELECT City FROM Clients
UNION
SELECT City FROM Suppliers;

SELECT City FROM Clients
INTERSECT
SELECT City FROM Suppliers;

SELECT City FROM Clients
EXCEPT   -- Use MINUS in Oracle
SELECT City FROM Suppliers;
```

---

## Q28: Explain the difference between Exclusive Lock and Update Lock

An Exclusive Lock (X lock) prevents other transactions from reading or modifying locked data until the lock is released, ensuring full isolation during write operations. It is acquired during DML changes (INSERT, UPDATE, DELETE) to maintain consistency and prevent concurrent changes. An Update Lock (U lock), meanwhile, is a transitional lock obtained when SQL Server intends to update data. It allows multiple transactions to read data (shared lock), but only one can promote to exclusive lock. Update locks reduce deadlocks by preventing two updates from holding shared locks and waiting for each other to escalate to exclusive locks.

```sql
-- Example: Acquiring exclusive lock
BEGIN TRAN
UPDATE Employees SET Salary = 60000 WHERE EmployeeID = 1;
-- At this point, data is exclusively locked

-- Update lock in action
SELECT * FROM Employees WITH (UPDLOCK)
WHERE EmployeeID = 1;
-- Now, intent to update is signaled to others
```

---

# Expert

## Q29: How does B-trees Index work?

A B-tree (Balanced Tree) index organizes data in a hierarchical structure, enabling efficient searches, insertions, and deletions. The tree consists of nodes (blocks/pages) that contain ordered keys, with the root at the top, intermediate nodes, and leaf nodes at the bottom containing actual pointers to table rows. Each non-leaf node acts as a guide, containing key ranges that route searches, minimizing the number of reads (O(log n) complexity). B-trees keep the tree balanced so all paths from root to leaf are the same length, ensuring consistent performance. They're suited for range queries, equality lookups, and maintaining sorted order, making them widely used in databases.

```sql
-- Automatically maintained with PRIMARY KEY or INDEX
CREATE INDEX idx_name ON Employees(LastName);
-- This creates a B-tree structure for fast searches.
```

---

## Q30: Name some disadvantages of a Hash index

Hash indexes, while fast for exact matches, have several disadvantages. They do not support range queries, sorting, or partial matching (like 'greater than' or 'like' conditions). Collisions—where different values map to the same hash—can degrade performance. Hash indexes generally require knowledge of the entire key for lookups. Updates and deletions can become inefficient if many collisions exist. They’re also less space-efficient due to potential for sparse mappings. If the hash function isn't well chosen or the data distribution is uneven, performance suffers. Most traditional RDBMSs use B-tree indexes for these reasons.

```sql
-- Example of hash-like index (in-memory optimized table in SQL Server)
CREATE TABLE MyTable (
    ID INT PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 100000)
);
```

---

## Q31: What are some other types of Indexes (vs B-Trees)?

Other than B-tree indexes, common types include Hash indexes (for fast equality queries), Bitmap indexes (efficient for low-cardinality columns), Full-Text indexes (for word/phrase search), Spatial indexes (for geographic data, e.g., R-Trees, QuadTrees), XML indexes (for XML data), and Columnstore indexes (for analytical queries, storing columns instead of rows for high compression and scanning speed). Each type benefits specific workloads and queries. For example, hash for in-memory and exact key search, bitmap for analytics, spatial for maps/geodata, and columnstore for data warehousing.

```sql
-- Bitmap index (Oracle)
CREATE BITMAP INDEX idx_active ON Employees(IsActive);

-- Columnstore index (SQL Server)
CREATE COLUMNSTORE INDEX idx_colstore ON Sales(SaleDate, Amount);
```

---

## Q32: How does database Indexing work?

Indexing creates data structures (like B-trees, Bitmaps, Hashes) that allow rapid lookup of rows based on column values, reducing the amount of data scanned during queries. When a query is executed, the optimizer determines if an index exists for the columns in conditions (WHERE, JOIN, etc.). Instead of scanning the entire table, the database navigates the index to quickly locate relevant row pointers, fetches only those rows, and returns results. Indexes maintain sorted or hashed representations enabling efficient searches, but must be updated when underlying data changes. Proper index design can drastically speed up data retrieval.

```sql
-- Create index for fast lookup
CREATE INDEX idx_email ON Users(Email);
-- Now SELECT ... WHERE Email = 'abc@example.com' uses the index.
```

---

## Q33: What is Optimistic Locking and Pessimistic Locking?

Optimistic Locking assumes data conflicts are rare; it allows concurrent data access without locks, checking for conflicts only when changes are saved (typically by comparing timestamps or version numbers). If the data was changed since it was read, the update is rejected. Pessimistic Locking locks data when it's read for update, blocking others until the transaction finishes, ensuring no conflicting writes occur. Optimistic is efficient for low-contention environments and scales well, while pessimistic ensures safety at the expense of concurrency, suitable for high-contention contexts.

```sql
-- Optimistic scenario
UPDATE Products SET Price = 50, Version=Version+1
WHERE ProductID = 1 AND Version = @OldVersion;

-- Pessimistic scenario
BEGIN TRAN
SELECT * FROM Products WITH (UPDLOCK) WHERE ProductID = 1;
UPDATE Products SET Price = 50 WHERE ProductID = 1;
COMMIT;
```

---

## Q34: What is the difference between B-Tree, R-Tree and Hash indexing?

B-Tree indexes arrange data in hierarchically sorted nodes, enabling fast lookups and range queries; they’re general-purpose and suit most workloads. R-Tree indexes are designed for spatial/multidimensional data, storing rectangles/n-dimensional objects and allowing efficient searches for ranges, overlaps, and proximity (geographic or geometric queries). Hash indexes compute a hash function on keys, allowing constant time lookups for exact matches but not supporting range or ordered queries. Each index type is optimal for its specific data access patterns.

```sql
-- B-tree index (general SQL)
CREATE INDEX idx_lastname ON Employees(LastName);

-- R-tree index (for spatial data, e.g., PostGIS)
CREATE INDEX idx_geometry ON Parcels USING GIST (geom);

-- Hash index (SQL Server In-Memory OLTP)
CREATE TABLE t(Id INT PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000));
```

---

## Q35: What is Index Cardinality and why does it matter?

Index cardinality refers to the uniqueness of values in the indexed column(s). High cardinality means many unique values (e.g., email addresses), while low cardinality means few distinct values (e.g., gender). High-cardinality indexes are most effective for accelerating searches, as they precisely narrow down result sets. Low-cardinality indexes often don’t offer significant speed benefits and can add unnecessary overhead. Query optimizers use cardinality statistics to decide when to use available indexes for best performance. Understanding cardinality is crucial for effective index design and query optimization.

```sql
-- High Cardinality: good for indexing
CREATE INDEX idx_email ON Users(Email);

-- Low Cardinality (might not help)
CREATE INDEX idx_status ON Orders(Status);  -- Only a few statuses exist
```
---