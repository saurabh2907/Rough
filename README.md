SELECT 
    DATEADD(MONTH, CAST(SUBSTRING([Accounting Period], 5, 2) AS INT) + 2, 
    CAST(SUBSTRING([Accounting Period], 1, 4) + '0101' AS DATE)) AS FinDate
FROM 
    Premium_Dump
