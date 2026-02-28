# CDC
CDC (Change Data Capture) is a technique to capture only the changes (INSERT, UPDATE, DELETE) made in a database instead of loading full data every time.  In Azure, CDC is commonly used for incremental data pipelines in data engineering.

--EXEC sys.sp_cdc_enable_db
--GO

CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,        -- Primary key column
    EmployeeName NVARCHAR(100),        -- Employee name column
    EmployeeDepartment NVARCHAR(50)    -- Employee department column
);

EXEC sys.sp_cdc_enable_table
    @source_schema = N'dbo',           -- Schema of the table
    @source_name   = N'Employee',      -- Name of the table
    @role_name     = NULL,             -- Role with access to the CDC tables (NULL for public access)
    @supports_net_changes = 1;
GO

CREATE TABLE Employee_Copy (
    EmployeeID INT PRIMARY KEY,        -- Primary key column
    EmployeeName NVARCHAR(100),        -- Employee name column
    EmployeeDepartment NVARCHAR(50)    -- Employee department column
);

INSERT INTO Employee (EmployeeID, EmployeeName, EmployeeDepartment)
VALUES
(1, 'John Doe', 'HR'),
(2, 'Jane Smith', 'Finance'),
(3, 'Mike Johnson', 'IT');
GO

UPDATE Employee
SET EmployeeName = 'Johnathan Doe',
    EmployeeDepartment = 'Human Resources'
WHERE EmployeeID = 1;
GO

DELETE FROM Employee
WHERE EmployeeID = 2;
GO
