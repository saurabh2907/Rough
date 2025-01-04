-- Step 1: Declare a variable to hold the comma-separated list of POL_No values
DECLARE @PolNoList NVARCHAR(MAX);

-- Step 2: Construct the comma-separated list of POL_No values
SELECT @PolNoList = STRING_AGG(CONVERT(NVARCHAR(MAX), POL_No), ',')
FROM #temp;

-- Step 3: Construct the dynamic SQL query
DECLARE @SQL NVARCHAR(MAX);
SET @SQL = N'SELECT POLICY_REF, BOOKING_FREQUENCY 
             FROM OPENQUERY([MISPROD1], 
             ''SELECT POLICY_REF, BOOKING_FREQUENCY 
               FROM OWB_ADMIN.FACT_POLICY_VW 
               WHERE POL_REF IN (' + @PolNoList + N')'')';

-- Step 4: Execute the dynamic SQL query
EXEC sp_executesql @SQL;
