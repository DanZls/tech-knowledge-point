# Entry

## Q1: Mention what is TOP in T-SQL?

TOP is a keyword in T-SQL used to limit the number of rows returned in a query result. It is especially useful when you only need a subset of rows for performance reasons or to retrieve samples. Often used with ORDER BY, TOP helps in scenarios like paging, selecting the highest/lowest values, or when only a fixed number of records are needed. TOP can accept a constant or a parameter and can also specify a PERCENT to retrieve a percentage of rows rather than a fixed number. The TOP clause is specific to T-SQL and may not be supported or may differ in other SQL dialects, where LIMIT or FETCH FIRST is used instead.

```sql
SELECT TOP 5 * FROM Sales ORDER BY SaleDate DESC;
SELECT TOP 10 PERCENT * FROM Customers;
```
---

## Q2: Is it possible to rename a database? If so, how would you rename the database?

Yes, it is possible to rename a database in SQL Server. The most common method is using the ALTER DATABASE statement with MODIFY NAME. It is important to ensure that no users are connected to the database when renaming, otherwise the statement might fail. The database should be set to single-user mode if in active use. Renaming a database will not update references within stored procedures, views, or application code, so thorough review is needed post-rename.

```sql
ALTER DATABASE OldDBName MODIFY NAME = NewDBName;
-- Or using sp_renamedb (deprecated, not recommended)
EXEC sp_renamedb 'OldDBName', 'NewDBName';
```
---

# Junior

## Q3: What is Blocking?

Blocking occurs in SQL Server when one connection (session) holds a lock on a resource, such as a row or table, and another connection attempts to acquire a conflicting lock type on the same resource but must wait. This is normal behavior to preserve data integrity under concurrent access, but excessive blocking can impact performance. Blocking is different from deadlocks; blocking eventually clears when the blocking transaction completes, while deadlocks must be resolved by terminating one transaction. Monitoring blocking helps identify problematic queries or transactions and tuning can minimize its impact.

```sql
-- Example: Session 1
BEGIN TRAN;
UPDATE Products SET Price = Price + 1 WHERE ProductID = 1;

-- Session 2 (will be blocked)
UPDATE Products SET Price = Price + 2 WHERE ProductID = 1;
```
---

## Q4: What is the difference between Data Definition Language (DDL) and Data Manipulation Language (DML)?

DDL consists of SQL commands that define and modify database schema and structure, such as CREATE, ALTER, and DROP. These affect the metadata. DML comprises commands that manage data inside schema objects, enabling you to SELECT, INSERT, UPDATE, and DELETE records. DDL changes are typically auto-committed, meaning once executed, they cannot be rolled back. DML operations can usually be rolled back as they are transactional.

```sql
-- DDL
CREATE TABLE Employees (ID INT, Name NVARCHAR(50));
ALTER TABLE Employees ADD BirthDate DATE;

-- DML
INSERT INTO Employees VALUES (1, 'John Doe', '1990-01-01');
UPDATE Employees SET Name = 'Jane Doe' WHERE ID = 1;
```
---

## Q5: Mention what is OFFSET-FETCH filter in T-SQL?

OFFSET-FETCH is a T-SQL clause used for pagination, introduced in SQL Server 2012. It allows skipping a specified number of rows (OFFSET) and then returning the next set (FETCH NEXT n ROWS ONLY), often used for displaying data page by page or for batch processing. It must be used with ORDER BY to ensure consistent results. Commonly used in web or app result pages to reduce data transmission and processing.

```sql
SELECT * FROM Orders
ORDER BY OrderDate DESC
OFFSET 10 ROWS FETCH NEXT 5 ROWS ONLY;
```
---

## Q6: Mention what is Subquery?

A subquery is a query nested inside another query, which can be used in SELECT, INSERT, UPDATE, DELETE, or within clauses like WHERE, FROM, or HAVING. Subqueries return single values (scalar), multiple rows, or entire result sets, and may be correlated (depending on the outer query) or non-correlated. They help break complex problems into simpler steps and encapsulate logic.

```sql
SELECT Name FROM Employees
WHERE DepartmentID = (SELECT DepartmentID FROM Departments WHERE Name = 'IT');
```
---

## Q7: What are the two commands to remove all of the data from a table? Are there any implications with the specific commands?

The two commands are DELETE and TRUNCATE. DELETE removes rows one at a time and logs each row, making it slower but allowing WHERE filters and triggers to fire. TRUNCATE removes all rows by deallocating data pages, is minimally logged, and much faster, but cannot be used with tables referenced by foreign keys or with enabled triggers. TRUNCATE also resets identity columns (in SQL Server), while DELETE does not.

```sql
DELETE FROM Employees; -- logs individual deletions, can use filters

TRUNCATE TABLE Employees; -- faster, resets identity, can't have foreign key constraints
```
---

## Q8: What are the three ways that Dynamic SQL can be issued?

Dynamic SQL allows executing SQL statements constructed at runtime. In T-SQL, it can be issued using:
1. EXEC (or EXECUTE) with a string parameter.
2. sp_executesql for parameterized execution, allowing reuse and safer passing of parameters.
3. Constructing and executing SQL inside procedures or scripts with EXEC or sp_executesql in dynamic scripts.

sp_executesql is generally preferred for safety and performance via query plan reuse.

```sql
-- Using EXEC
EXEC('SELECT * FROM Customers');

-- Using sp_executesql
DECLARE @sql NVARCHAR(MAX) = N'SELECT * FROM Customers WHERE City = @City';
EXEC sp_executesql @sql, N'@City NVARCHAR(50)', @City = 'London';
```
---

## Q9: Mention what are the limitations of IDENTITY column?

IDENTITY columns auto-increment values but have several limitations:
- Only one identity column per table.
- Cannot update or insert explicit values unless IDENTITY_INSERT is ON.
- Can cause gaps in sequence if transactions are rolled back.
- Value resets only with TRUNCATE, not on DELETE.
- Does not guarantee gap-free values or replication consistency.
- Reseeding possible, but may have concurrency issues.

```sql
CREATE TABLE Products (ProductID INT IDENTITY(1,1), Name NVARCHAR(50));

-- Cannot force a value unless:
SET IDENTITY_INSERT Products ON;
INSERT INTO Products (ProductID, Name) VALUES (100, 'Special Product');
SET IDENTITY_INSERT Products OFF;
```
---

## Q10: What’s the difference between a Local Temp Table and a Global Temp Table?

Local Temp Tables are prefixed with #, only visible to the session that created them, and are dropped automatically when the session ends. Global Temp Tables are prefixed with ##, visible to any session, and persist until all sessions referencing them are closed. Local temp tables help with session or process-scoped temporary storage; global temp tables share temporary data across sessions but can cause conflicts.

```sql
-- Local Temp Table
CREATE TABLE #TempLocal (ID INT);

-- Global Temp Table
CREATE TABLE ##TempGlobal (ID INT);
```
---

## Q11: When should I use primary key or index?

A primary key enforces entity integrity, ensures uniqueness, and automatically creates a clustered index (unless otherwise specified). Use a primary key whenever you must uniquely identify table rows. Indexes, whether unique or not, are used for fast data retrieval and do not guarantee uniqueness unless defined as unique. Use indexes for query performance where uniqueness isn't required or for frequently searched columns. Multiple indexes can exist per table, but only one primary key.

```sql
-- Primary Key
CREATE TABLE Employees (ID INT PRIMARY KEY, Name NVARCHAR(50));

-- Non-unique index
CREATE INDEX idx_EmployeeName ON Employees(Name);
```
---

## Q12: Name 5 commands that can be used to manipulate text in T-SQL code

1. LEFT(): Returns the left part of a string.
2. RIGHT(): Returns the right part of a string.
3. SUBSTRING(): Extracts a substring from a string.
4. REPLACE(): Replaces all occurrences of a substring.
5. LEN(): Returns the length of a string.

```sql
SELECT LEFT('abcdef', 3);      -- 'abc'
SELECT RIGHT('abcdef', 2);     -- 'ef'
SELECT SUBSTRING('abcdef', 2, 3); -- 'bcd'
SELECT REPLACE('abc abc', 'a', 'x');  -- 'xbc xbc'
SELECT LEN('abcdef');          -- 6
```
---

## Q13: Could you explain the difference between Primary Key and Unique Index?

Primary Key:
- Enforces entity integrity (cannot be NULL, unique).
- Only one per table.
- Automatically creates a clustered index by default.
- Used for row identification.

Unique Index:
- Allows multiple per table.
- Can accept NULLs (except in SQL Server for columns with unique constraint).
- Restricts duplicate values but is not intended as a row identifier.
- Does not imply clustering.

```sql
-- Primary Key
CREATE TABLE Users (UserID INT PRIMARY KEY, Email NVARCHAR(100));

-- Unique Index
CREATE UNIQUE INDEX IX_Users_Email ON Users(Email);
```
---

## Q14: What are the new error handling commands introduced with SQL Server 2005 and beyond?

TRY...CATCH was introduced in SQL Server 2005, allowing structured exception handling. You can capture error information using ERROR_NUMBER(), ERROR_MESSAGE(), etc., within the CATCH block. THROW was introduced in SQL Server 2012 to re-raise errors or raise custom exceptions, providing more control over error propagation.

```sql
BEGIN TRY
    -- code that may fail
    SELECT 1/0;
END TRY
BEGIN CATCH
    SELECT ERROR_MESSAGE() AS ErrorMsg;
END CATCH

-- Using THROW
THROW 50000, 'Custom error message', 1;
```
---

## Q15: Explain what are the differences between SQL and T-SQL?

SQL (Structured Query Language) is the ANSI standard for managing relational databases—providing commands for CRUD (select, insert, update, delete) and schema definitions. T-SQL (Transact-SQL) is Microsoft’s proprietary extension, adding procedural programming, error handling, local variables, transactions, custom functions, and system functions. T-SQL includes constructs like DECLARE, TRY...CATCH, WHILE, and system stored procedures, and supports dynamic SQL.

```sql
-- Standard SQL
SELECT * FROM Employees;

-- T-SQL extension
DECLARE @Name NVARCHAR(50);
SET @Name = 'John';
SELECT * FROM Employees WHERE Name = @Name;
```
---

## Q16: What is TSQL Window functions?

Window functions perform calculations across sets of rows related to the current row, without collapsing result sets as GROUP BY does. Examples are ROW_NUMBER(), RANK(), DENSE_RANK(), SUM(), AVG() OVER(). They require an OVER() clause, optionally partitioned or ordered by, allowing calculations like running totals, moving averages, or ranking without aggregates.

```sql
SELECT Name,
       Salary,
       ROW_NUMBER() OVER (ORDER BY Salary DESC) AS Rank
FROM Employees;
```
---

# Mid

## Q17: What is a Cursor and how does it work?

A cursor is a T-SQL database object allowing row-by-row processing of query results. It works by opening a result set, fetching rows sequentially, and providing operations for FETCH, UPDATE, and DELETE at the current position. Cursors can be explicit or implicit, static (snapshot), dynamic (reflects data changes), forward-only, and can be read-only or updatable. They are useful for complex logic not possible with set-based operations, but cursors are resource-intensive and should be used sparingly.

```sql
DECLARE cursor_example CURSOR FOR
    SELECT Name FROM Employees;
OPEN cursor_example;
FETCH NEXT FROM cursor_example INTO @Name;
-- Process each row
CLOSE cursor_example;
DEALLOCATE cursor_example;
```
---

## Q18: What’s the difference between Azure SQL Database and Azure SQL Managed Instance?

Azure SQL Database is a cloud-based single-database or elastic pool solution, providing managed resources, automatic scalability, and auto-patching, but with limited on-premises features. Azure SQL Managed Instance offers near-complete SQL Server compatibility, supporting cross-database queries, SQL Agent, Service Broker, and linked servers, making it suitable for lifting and shifting on-premises workloads with minimal modification. Managed Instance provides more control and features closer to full SQL Server.

```sql
-- No code, conceptual differences only.
```
---

## Q19: What are the advantages of using Stored Procedures?

Stored Procedures offer several benefits:
- Improved performance via execution plan reuse.
- Enhanced security by abstracting underlying tables and limiting direct table access.
- Centralized, reusable logic, making maintenance easier.
- Reduced network traffic through batch execution.
- Support for input/output parameters, implementing business rules.
- Easier permission management.
- Versioning and auditing for business operations.

```sql
CREATE PROCEDURE usp_GetEmployees @DeptID INT
AS
BEGIN
    SELECT * FROM Employees WHERE DepartmentID = @DeptID;
END;
```
---

## Q20: What are bitwise operators and what is the value from a database design perspective?

Bitwise operators (|, &, ~, ^) allow manipulation of individual bits within an integer. In SQL Server, they can be used to store multiple boolean values in a single column using flag fields, saving space and simplifying schema when only a few true/false states are needed. However, overuse reduces readability and query simplicity, and complicates indexing and reporting.

```sql
-- Store and check flags
-- Assume Flag column INT, '1' for active, '2' for verified
UPDATE Users SET Flag = Flag | 2 WHERE UserID = 1; -- Set verified
SELECT * FROM Users WHERE (Flag & 2) = 2;          -- Select verified
```
---

## Q21: Mention what are ROLLUP and CUBE in T-SQL?

ROLLUP and CUBE are GROUP BY extensions for multidimensional aggregations. ROLLUP generates hierarchical totals by progressively grouping columns, so you get subtotals and grand totals. CUBE computes all possible combinations of groupings (cross-tabulation), providing more extensive summary data. Both are used in analytics and reporting scenarios.

```sql
-- ROLLUP: Department subtotal, then grand total
SELECT Department, Year, SUM(Sales)
FROM SalesData
GROUP BY ROLLUP (Department, Year);

-- CUBE: all combinations
SELECT Department, Year, SUM(Sales)
FROM SalesData
GROUP BY CUBE (Department, Year);
```
---

## Q22: How do I perform an IF…THEN in an SQL SELECT?

Unlike procedural programming, SQL SELECT can’t use IF...THEN directly. Instead, use CASE expressions to implement conditional logic within SELECT, WHERE, ORDER BY, etc. The CASE statement evaluates conditions and returns results accordingly.

```sql
SELECT Name,
       Salary,
       CASE WHEN Salary > 50000 THEN 'High' ELSE 'Low' END AS SalaryLevel
FROM Employees;
```
---

## Q23: What’s the difference between TRUNCATE and DELETE in SQL?

TRUNCATE quickly removes all rows by deallocating data pages, is minimally logged, and cannot have a WHERE clause or fire triggers. It also resets identity columns. DELETE removes rows one by one, logs each deletion, allows WHERE filtering, and fires triggers. TRUNCATE is faster for clearing tables but has restrictions regarding foreign keys and triggers.

```sql
TRUNCATE TABLE MyTable; -- Fast, resets identity
DELETE FROM MyTable WHERE Age > 60; -- Filtered, logs rows, triggers fire
```
---

## Q24: How can you delete duplicate records in a table with no primary key?

You can use a CTE with ROW_NUMBER() to assign a unique row number for each duplicate group based on columns that define uniqueness. Then, delete all but the row with row number 1.

```sql
WITH CTE AS (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY Col1, Col2 ORDER BY (SELECT 0)) AS rn
  FROM MyTable
)
DELETE FROM CTE WHERE rn > 1;
```
---

## Q25: Mention what are the Join Types in TSQL?

T-SQL supports these join types:
- INNER JOIN: Returns only matching rows from both tables.
- LEFT OUTER JOIN: Returns all rows from the left table, plus matches from the right table if any.
- RIGHT OUTER JOIN: All rows from the right, and matches from the left.
- FULL OUTER JOIN: All rows from both tables, combining matches.
- CROSS JOIN: Cartesian product, all combinations of rows.
- SELF JOIN: Joins a table to itself to traverse hierarchical data.

```sql
SELECT * FROM A INNER JOIN B ON A.ID = B.AID;
SELECT * FROM A LEFT OUTER JOIN B ON A.ID = B.AID;
SELECT * FROM A RIGHT OUTER JOIN B ON A.ID = B.AID;
SELECT * FROM A FULL OUTER JOIN B ON A.ID = B.AID;
SELECT * FROM A CROSS JOIN B;
```
---

## Q26: What are types of XML indexes in SQL Server?
SQL Server offers two primary types of indexes for XML data: primary XML indexes and secondary XML indexes. A primary XML index is built on an XML column and shreds XML BLOBs into multiple internal tables, optimizing queries that retrieve XML data or use XML methods. Secondary XML indexes are created on top of the primary XML index to optimize specific types of XML queries. There are three main secondary XML indexes: PATH (optimizes queries using the exist() and nodes() methods), VALUE (speeds up value(), query(), and cast() operations), and PROPERTY (boosts performance for property access via dot notation). You must create a primary XML index before you can create any secondary XML indexes. Proper indexing improves XML query performance but can increase storage and maintenance overhead.
```sql
-- Create a primary XML index
CREATE PRIMARY XML INDEX idx_XML_Primary 
ON dbo.MyTable(XmlColumn);

-- Create secondary XML indexes
CREATE XML INDEX idx_XML_Path
ON dbo.MyTable(XmlColumn)
USING XML INDEX idx_XML_Primary
FOR PATH;

CREATE XML INDEX idx_XML_Value
ON dbo.MyTable(XmlColumn)
USING XML INDEX idx_XML_Primary
FOR VALUE;
```
---

## Q27: What two commands were released in SQL Server 2005 related to comparing data sets from two or more separate SELECT statements?
SQL Server 2005 introduced the INTERSECT and EXCEPT set operators, which facilitate data set comparison. INTERSECT returns all distinct rows produced by both SELECT statements, effectively giving the common records between result sets. EXCEPT returns all distinct rows from the first SELECT statement that do not appear in the second, functioning like a “difference” operation. These operators are similar to their mathematical set counterparts and require that both queries have the same number and order of columns, with compatible data types. Using these commands helps simplify queries that would otherwise need complex joins or subqueries for set-based comparisons.
```sql
-- Using INTERSECT
SELECT column1 FROM TableA
INTERSECT
SELECT column1 FROM TableB;

-- Using EXCEPT
SELECT column1 FROM TableA
EXCEPT
SELECT column1 FROM TableB;
```
---

## Q28: Mention what is uncommittable transactions?
An uncommittable transaction is a transaction that cannot be committed to the database, typically due to an error during execution. In SQL Server, if an error occurs that is severe enough (for example, a constraint violation), the transaction enters an uncommittable state. No further successful COMMIT operations are allowed unless a ROLLBACK is issued first. This often happens within TRY...CATCH error handling blocks when XACT_STATE() = -1, indicating that the transaction must be rolled back. Not handling uncommittable transactions properly may lead to locks being held for longer periods and resource contention.
```sql
BEGIN TRANSACTION
    BEGIN TRY
        -- Code that causes an error
        INSERT INTO MyTable(Id) VALUES(NULL);
        COMMIT TRANSACTION;
    END TRY
    BEGIN CATCH
        IF (XACT_STATE()) = -1
            ROLLBACK TRANSACTION;
    END CATCH
```
---

## Q29: What are Row Constructors?
Row constructors, introduced in SQL Server 2008, let you specify multiple rows of values in a single INSERT statement. With the VALUES clause, you can insert several rows at once, making data insertion more concise, readable, and faster than repeating separate INSERT statements. This feature also appears in other operations including the use of the VALUES clause with table-valued constructors for comparison and joins. It helps to simplify code, improve performance, and reduce server round-trips.
```sql
INSERT INTO Employees (Name, Department)
VALUES ('Alice', 'HR'),
       ('Bob', 'Finance'),
       ('Carol', 'IT');
```
---

## Q30: In what version of SQL Server were synonyms released, what do synonyms do and when could you make the case for using them?
Synonyms were introduced in SQL Server 2005. They act as alternative names for database objects such as tables, views, procedures, or functions, potentially on local or remote servers. Synonyms provide abstraction, making it easier to reference objects without hardcoding their full names or locations, which aids in code portability and maintenance. A common use case is when an underlying object’s location or name changes: only the synonym needs updating, not all referencing code. Synonyms also simplify access to objects across databases or linked servers.
```sql
CREATE SYNONYM MyEmp 
FOR HRDatabase.dbo.Employees;
-- Now you can use MyEmp as an alias in queries:
SELECT * FROM MyEmp;
```
---

## Q31: Is there a difference between T-SQL linked server and a synonym?
Yes, T-SQL linked servers and synonyms serve different purposes but can work together. A linked server allows SQL Server to connect and execute queries against external data sources, whether another SQL Server or a different DBMS, enabling distributed queries. A synonym, on the other hand, is a local database alias for a database object, which can reference objects located via a linked server. So, a synonym provides a local name, while a linked server handles remote connections. You often use synonyms to simplify referencing objects over linked servers.
```sql
-- Create a linked server
EXEC sp_addlinkedserver 'RemoteServer', 'SQL Server';

-- Create a synonym for a remote table via linked server
CREATE SYNONYM RemoteEmp 
FOR RemoteServer.Database.dbo.Employees;
```
---

## Q32: Mention what does the T-SQL command IDENT_CURRENT does?
IDENT_CURRENT is a T-SQL function that returns the last identity value generated for a specific table in any session and scope. Unlike SCOPE_IDENTITY(), which is limited to the current session and scope, IDENT_CURRENT retrieves the most recent identity value regardless of connection or process. This behavior makes it useful for auditing and integration tasks, but risky for retrieving values after inserts in multi-user environments since it might not represent the value just created by your session.
```sql
SELECT IDENT_CURRENT('Employees') AS LastIdentity;
```
---

## Q33: Explain Function vs. Stored Procedure in SQL Server
In SQL Server, a Function (UDF) must return a value (scalar or table), can be used within SELECT statements, and cannot perform transactional changes or call stored procedures. Stored Procedures do not have a return type, can perform data modification and transactional operations, and can return zero, one, or multiple result sets. Procedures support output parameters, error handling, and can invoke dynamic SQL or other procedures, offering greater flexibility, but cannot be directly used in SELECT queries.
```sql
-- Function
CREATE FUNCTION fn_GetEmployeeName(@EmpId INT)
RETURNS VARCHAR(50)
AS
BEGIN
    RETURN (SELECT Name FROM Employees WHERE Id = @EmpId);
END

-- Stored Procedure
CREATE PROCEDURE sp_GetEmployeeName
    @EmpId INT
AS
BEGIN
    SELECT Name FROM Employees WHERE Id = @EmpId;
END
```
---

## Q34: What are the practical differences between COALESCE() and ISNULL('')?
COALESCE() and ISNULL() are both used to handle NULL values but have differences. ISNULL() is specific to SQL Server, accepts exactly two arguments, and returns the data type of the first argument. COALESCE() is ANSI SQL standard, accepts multiple arguments, and returns the data type with the highest precedence. COALESCE can be used in cross-platform scenarios and is preferable when evaluating more than two expressions. ISNULL evaluates only the first two values and is often slightly faster in SQL Server due to its design.
```sql
SELECT ISNULL(NULL, 'fallback');        -- Returns 'fallback'
SELECT COALESCE(NULL, NULL, 'x');       -- Returns 'x'
```
---

## Q35: Is it possible to import data directly from T-SQL commands without using SQL Server Integration Services? If so, what are the commands?
Yes, you can import data directly via T-SQL using commands such as BULK INSERT, OPENROWSET, and bcp utility (via xp_cmdshell). BULK INSERT reads data from a file into a table. OPENROWSET can import data from various sources, including files and OLEDB data providers (subject to configuration). These methods are efficient for bulk data loads without needing SSIS.
```sql
BULK INSERT dbo.MyTable
FROM 'C:\data\data.csv'
WITH (FIRSTROW = 2, FIELDTERMINATOR = ',', ROWTERMINATOR = '\n');

-- Or using OPENROWSET
INSERT INTO dbo.MyTable
SELECT * FROM OPENROWSET(
    BULK 'C:\data\data.csv',
    FORMATFILE = 'C:\data\format.fmt',
    FIRSTROW = 2
) AS DataFile;
```
---

## Q36: What is a Filegroup?
A filegroup in SQL Server is a logical container for database files that helps manage data allocation and placement. Each filegroup can contain one or more data files, and typically databases have a primary filegroup for system tables and user filegroups for user data. Filegroups enable administrators to separate data across multiple disks for performance or maintenance (e.g., backup/restore at the filegroup level), making them vital for large databases, partitioning, or managing I/O load.
```sql
-- Add a file to a filegroup
ALTER DATABASE MyDb
ADD FILE (
    NAME = N'MyDataFile2',
    FILENAME = N'D:\SQLData\MyDataFile2.ndf'
)
TO FILEGROUP MyFileGroup2;
```
---

# Senior

## Q37: What is the difference between PARTITION BY and GROUP BY?
PARTITION BY is used in window functions to divide result sets into partitions and perform calculations across those partitions (without collapsing rows). GROUP BY aggregates data, reducing multiple rows to a single row per group. Use PARTITION BY for calculations like running totals, rankings, or averages applied per group while keeping all rows. GROUP BY is for summarizing data with aggregation functions, returning fewer rows.
```sql
-- PARTITION BY (using window function)
SELECT Dept, Salary, AVG(Salary) OVER (PARTITION BY Dept) AS AvgDeptSalary
FROM Employees;

-- GROUP BY (aggregation)
SELECT Dept, AVG(Salary) AS AvgDeptSalary
FROM Employees
GROUP BY Dept;
```
---

## Q38: Name some types of Triggers
SQL Server supports several trigger types:
- DML triggers: Activated by INSERT, UPDATE, or DELETE on tables or views. They can be AFTER or INSTEAD OF triggers.
- DDL triggers: Respond to changes in schema, such as CREATE, ALTER, or DROP events.
- LOGON triggers: Fire when a user session is established.
Triggers can enforce business rules, audit changes, or control schema modifications.
```sql
-- DML Trigger
CREATE TRIGGER trg_AuditInsert
ON Employees
AFTER INSERT
AS
BEGIN
    -- Audit logic here
END

-- DDL Trigger
CREATE TRIGGER ddl_Audit
ON DATABASE
FOR CREATE_TABLE
AS
BEGIN
    -- Audit schema change
END
```
---

## Q39: What is the difference between EXEC vs sp_executesql?
EXEC executes a T-SQL command string or stored procedure, but with dynamic SQL, it passes variable values as simple string concatenation. sp_executesql executes dynamic SQL and allows parameterization, making it safer from SQL injection, promoting execution plan reuse, and easier to read and maintain. sp_executesql supports both input and output parameters, while EXEC does not natively support output parameters for dynamic SQL.
```sql
-- EXEC
EXEC('SELECT * FROM Employees WHERE Id = ' + @EmpId);

-- sp_executesql
DECLARE @SQL NVARCHAR(100) = N'SELECT * FROM Employees WHERE Id = @EmpId';
EXEC sp_executesql @SQL, N'@EmpId INT', @EmpId;
```
---

## Q40: What do Clustered and Non Clustered index actually mean?
A Clustered index determines the physical order of data within a table; table data is stored in the order of the clustered index key, and there's only one clustered index per table. A Non-Clustered index creates a separate structure with pointers to the actual data rows. Non-clustered indexes do not affect physical storage order, and you can have multiple per table. Clustered indexes are best for range queries; non-clustered indexes are suited for quicker lookups on columns not covered by the clustered index.
```sql
-- Clustered index
CREATE CLUSTERED INDEX idx_Clustered ON Employees(Id);

-- Non-clustered index
CREATE NONCLUSTERED INDEX idx_NonClustered ON Employees(Name);
```
---

## Q41: What is the use of GO in Transact SQL?
GO is a batch separator recognized by SQL Server Management Studio and command-line tools, not the SQL Server engine itself. It tells the tool to send the current batch of statements to the server for execution. GO helps separate logical units of code, such as variable declarations from usage or script sections that need to be executed separately. It is not a T-SQL command and cannot be used inside stored procedures or dynamic SQL.
```sql
-- Example with GO
CREATE TABLE Temp1 (Id INT);
GO
INSERT INTO Temp1 VALUES (1);
GO
```
---

## Q42: What is a Linked Server?
A Linked Server is a configuration in SQL Server that allows the engine to execute commands against OLE DB data sources outside the current instance. This capability enables distributed queries, updates, and joins across different servers (local or remote), as well as other data providers (e.g., Oracle, Access). Linked servers are managed with system stored procedures and are frequently used for data integration, migration, or cross-server reporting.
```sql
-- Add linked server
EXEC sp_addlinkedserver 'MyServer', 'SQL Server';
-- Query remote data
SELECT * FROM MyServer.Database.dbo.Table1;
```
---

# Expert

## Q43: From a T-SQL perspective, how would you prevent T-SQL code from running on a production SQL Server?
You can prevent T-SQL code from running in production by using server-level checks in scripts, such as querying @@SERVERNAME, DB_NAME(), or environment-specific flags, and then exiting or raising errors if a match is detected. You can also use configuration tables or environment variables as checks. This approach minimizes the risk of unintended destructive operations in live environments.
```sql
IF @@SERVERNAME = 'PROD-SERVER'
    BEGIN
        RAISERROR('Script cannot be run on production!', 16, 1);
        RETURN;
    END
```
---

## Q44: What is the native system stored procedure to issue a command against all databases?
sp_MSforeachdb is an undocumented but commonly used system stored procedure for executing a command against each database on an instance. It iterates through all user and system databases, inserting the database name as a placeholder in your command. While powerful, it is unsupported by Microsoft and may be deprecated in future versions, so use it with caution.
```sql
EXEC sp_MSforeachdb 'SELECT COUNT(*) AS NumTables FROM [?].sys.tables';
```
---

## Q45: What are the best practices for using a GUID as a primary key, specifically regarding performance?
While GUIDs offer global uniqueness, using them as primary keys brings performance concerns: they require more storage (16 bytes), generate random insert patterns (fragmenting indexes), and can slow join and search operations. To mitigate these, use sequential GUIDs (NEWSEQUENTIALID()), reduce index width, or use surrogate integer keys. Avoid using GUIDs as clustered indexes; if needed, keep them non-clustered. Monitor table size, fragmentation, and rebuild indexes as required. 
```sql
-- Create sequential GUID as default
CREATE TABLE Orders (
    OrderID UNIQUEIDENTIFIER DEFAULT NEWSEQUENTIALID() PRIMARY KEY,
    ...
);
```
---

## Q46: Why you should never use GUIDs as part of clustered index?
Using GUIDs in clustered indexes leads to high fragmentation, poor page usage, and random I/O, which hurts insert speed and disk performance. Since clustered indexes dictate row order, GUIDs’ randomness means new rows are inserted in arbitrary locations. This leads to inefficient disk access, larger indexes, and increased maintenance overhead. For best performance, use narrow, ever-increasing columns (e.g., INT IDENTITY) for clustered indexes and keep GUIDs non-clustered if necessary.
```sql
-- Non-clustered GUID index, with INT clustered index
CREATE TABLE MyTable (
    ID INT IDENTITY PRIMARY KEY CLUSTERED,
    MyGuid UNIQUEIDENTIFIER UNIQUE NONCLUSTERED
);
```
---

## Q47: Is it correct/best practice to have the TRY/CATCH block inside the transaction or should the transaction be inside the TRY block?
The best practice is to start the transaction inside the TRY block, not before it. This ensures that BEGIN TRANSACTION, COMMIT, and ROLLBACK are managed together, and that errors during transaction statements are caught. Starting the transaction outside may leave unhandled exceptions or uncommittable transactions if errors occur before TRY begins. Always check transaction state in the CATCH block with XACT_STATE() to determine the right action.
```sql
BEGIN TRY
    BEGIN TRANSACTION
    -- Operations
    COMMIT TRANSACTION
END TRY
BEGIN CATCH
    IF XACT_STATE() <> 0
        ROLLBACK TRANSACTION
    -- Handle error
END CATCH
```
---