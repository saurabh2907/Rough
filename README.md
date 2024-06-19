CREATE PROCEDURE ImportDailyPremRetailCSV
    @FilePath NVARCHAR(255)
AS
BEGIN
    -- Create a temporary table to hold the CSV data
    CREATE TABLE #DailyPremRetailCSV (
        [A Agent Code] Varchar(50) NULL,
	[Accounting Month] Varchar(50) NULL,
	[Annuity Option] Varchar(50) NULL,
	[Annulized] Varchar(50) NULL,
	[Appln No] Varchar(50) NULL,
	[As On Date] Varchar(50) NULL,
	[Benefit Term] Varchar(50) NULL,
	[Deferred Period] Varchar(50) NULL,
	[Ftd Rtd Premium] Varchar(50) NULL,
	[Full Term Premium] Varchar(50) NULL,
	[Main Channel] Varchar(50) NULL,
	[Maturity Date] Varchar(50) NULL,
	[Mph Name] Varchar(50) NULL,
	[Mph No] Varchar(50) NULL,
	[Package Code] Varchar(50) NULL,
	[Partner Id] Varchar(50) NULL,
	[Policy Holder Partid] Varchar(50) NULL,
	[Policy Ref] Varchar(50) NULL,
	[Premium Amount] Varchar(50) NULL,
	[Premium Amt] Varchar(50) NULL,
	[Premium Term] Varchar(50) NULL,
	[Product Id] Varchar(50) NULL,
	[Product Type] Varchar(50) NULL,
	[Rated Premium] Varchar(50) NULL,
	[Relationship Name] Varchar(200) NULL,
	[Sub Channel] Varchar(50) NULL,
	[Type Ind] Varchar(50) NULL,
	[Vertical] Varchar(50) NULL
        -- Add more columns as per your CSV structure
    );
	
    -- BULK INSERT to import the CSV data into the temporary table
    BULK INSERT #DailyPremRetailCSV
    FROM @FilePath
    WITH (
        FIELDTERMINATOR = ',',
        ROWTERMINATOR = '\n',
        FIRSTROW = 2 -- Assuming the first row contains column headers
    );

	TRUNCATE TABLE [FinDB].[dbo].[Daily_Premium_Retail1]
    -- Insert data into the actual table, ensuring data integrity
    INSERT INTO [FinDB].[dbo].[Daily_Premium_Retail1] ([A Agent Code] ,
	[Accounting Month] ,
	[Annuity Option] ,
	[Annulized] ,
	[Appln No] ,
	[As On Date] ,
	[Benefit Term] ,
	[Deferred Period] ,
	[Ftd Rtd Premium] ,
	[Full Term Premium] ,
	[Main Channel] ,
	[Maturity Date] ,
	[Mph Name] ,
	[Mph No] ,
	[Package Code] ,
	[Partner Id] ,
	[Policy Holder Partid] ,
	[Policy Ref] ,
	[Premium Amount] ,
	[Premium Amt] ,
	[Premium Term] ,
	[Product Id] ,
	[Product Type] ,
	[Rated Premium] ,
	[Relationship Name],
	[Sub Channel] ,
	[Type Ind],
	[Vertical])

    SELECT [A Agent Code] ,
	[Accounting Month] ,
	[Annuity Option] ,
	[Annulized] ,
	[Appln No] ,
	[As On Date] ,
	[Benefit Term] ,
	[Deferred Period] ,
	[Ftd Rtd Premium] ,
	[Full Term Premium] ,
	[Main Channel] ,
	[Maturity Date] ,
	[Mph Name] ,
	[Mph No] ,
	[Package Code] ,
	[Partner Id] ,
	[Policy Holder Partid] ,
	[Policy Ref] ,
	[Premium Amount] ,
	[Premium Amt] ,
	[Premium Term] ,
	[Product Id] ,
	[Product Type] ,
	[Rated Premium] ,
	[Relationship Name],
	[Sub Channel] ,
	[Type Ind],
	[Vertical]
    FROM #DailyPremRetailCSV


    -- Drop the temporary table
    DROP TABLE #DailyPremRetailCSV;
END;


