# CDC
CDC (Change Data Capture) is a technique to capture only the changes (INSERT, UPDATE, DELETE) made in a database instead of loading full data every time.  In Azure, CDC is commonly used for incremental data pipelines in data engineering.

-- Enable CDC on the database
EXEC sys.sp_cdc_enable_db;
GO
