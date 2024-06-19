CREATE PROCEDURE AUTO_LOAD
AS
BEGIN 

  -- Create table
    IF OBJECT_ID('sales') IS NOT NULL DROP TABLE sales
    CREATE TABLE sales(
      prod_id VARCHAR(6),
      qty INTEGER,
      price INTEGER,
      discount INTEGER,
      members VARCHAR(5),
      txn_id VARCHAR(6),
      start_txn_time DATETIME
    );

  -- Remove the old records from the table
    TRUNCATE TABLE sales;

  -- Load the data into the table from the CSV file
    BULK INSERT sales
    FROM 'C:\Users\Lenovo\Downloads\Files\sales3.csv'
    WITH (FORMAT = 'CSV', FIELDTERMINATOR = ';', 
ROWTERMINATOR = '\n', FIRSTROW = 2);

END;
