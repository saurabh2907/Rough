CREATE PROCEDURE ImportDailyPremRetailCSV
    @FilePath NVARCHAR(255)
AS
BEGIN
    -- Create a temporary table to hold the CSV data
    CREATE TABLE #DailyPremRetailCSV (
        [A Agent Code] VARCHAR(50) NULL,
        [Accounting Month] VARCHAR(50) NULL,
        [Annuity Option] VARCHAR(50) NULL,
        [Annulized] VARCHAR(50) NULL,
        [Appln No] VARCHAR(50) NULL,
        [As On Date] VARCHAR(50) NULL,
        [Benefit Term] VARCHAR(50) NULL,
        [Deferred Period] VARCHAR(50) NULL,
        [Ftd Rtd Premium] VARCHAR(50) NULL,
        [Full Term Premium] VARCHAR(50) NULL,
        [Main Channel] VARCHAR(50) NULL,
        [Maturity Date] VARCHAR(50) NULL,
        [Mph Name] VARCHAR(50) NULL,
        [Mph No] VARCHAR(50) NULL,
        [Package Code] VARCHAR(50) NULL,
        [Partner Id] VARCHAR(50) NULL,
        [Policy Holder Partid] VARCHAR(50) NULL,
        [Policy Ref] VARCHAR(50) NULL,
        [Premium Amount] VARCHAR(50) NULL,
        [Premium Amt] VARCHAR(50) NULL,
        [Premium Term] VARCHAR(50) NULL,
        [Product Id] VARCHAR(50) NULL,
        [Product Type] VARCHAR(50) NULL,
        [Rated Premium] VARCHAR(50) NULL,
        [Relationship Name] VARCHAR(200) NULL,
        [Sub Channel] VARCHAR(50) NULL,
        [Type Ind] VARCHAR(50) NULL,
        [Vertical] VARCHAR(50) NULL
        -- Add more columns as per your CSV structure
    );

    -- Dynamic SQL for BULK INSERT to import the CSV data into the temporary table
    DECLARE @SQL NVARCHAR(MAX);
    SET @SQL = N'BULK INSERT #DailyPremRetailCSV
                 FROM ''' + @FilePath + '''
                 WITH (
                     FIELDTERMINATOR = '','',
                     ROWTERMINATOR = ''\n'',
                     FIRSTROW = 2 -- Assuming the first row contains column headers
                 )';
    
    EXEC sp_executesql @SQL;

    -- Truncate the destination table before inserting new data
    TRUNCATE TABLE [FinDB].[dbo].[Daily_Premium_Retail1];

    -- Insert data into the actual table, ensuring data integrity
    INSERT INTO [FinDB].[dbo].[Daily_Premium_Retail1] (
        [A Agent Code],
        [Accounting Month],
        [Annuity Option],
        [Annulized],
        [Appln No],
        [As On Date],
        [Benefit Term],
        [Deferred Period],
        [Ftd Rtd Premium],
        [Full Term Premium],
        [Main Channel],
        [Maturity Date],
        [Mph Name],
        [Mph No],
        [Package Code],
        [Partner Id],
        [Policy Holder Partid],
        [Policy Ref],
        [Premium Amount],
        [Premium Amt],
        [Premium Term],
        [Product Id],
        [Product Type],
        [Rated Premium],
        [Relationship Name],
        [Sub Channel],
        [Type Ind],
        [Vertical]
    )
    SELECT 
        [A Agent Code],
        [Accounting Month],
        [Annuity Option],
        [Annulized],
        [Appln No],
        [As On Date],
        [Benefit Term],
        [Deferred Period],
        [Ftd Rtd Premium],
        [Full Term Premium],
        [Main Channel],
        [Maturity Date],
        [Mph Name],
        [Mph No],
        [Package Code],
        [Partner Id],
        [Policy Holder Partid],
        [Policy Ref],
        [Premium Amount],
        [Premium Amt],
        [Premium Term],
        [Product Id],
        [Product Type],
        [Rated Premium],
        [Relationship Name],
        [Sub Channel],
        [Type Ind],
        [Vertical]
    FROM #DailyPremRetailCSV;

    -- Drop the temporary table
    DROP TABLE #DailyPremRetailCSV;
END;







SELECT
    OriginalDate,
    CONVERT(NVARCHAR(10), DATEFROMPARTS(CONVERT(INT, LEFT(OriginalDate, 4)), CONVERT(INT, RIGHT(OriginalDate, 3)), 1), 120) AS FormattedDate
FROM
    YourTableName;
