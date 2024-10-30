SELECT 
    DATEADD(MONTH, 
            (CAST(SUBSTRING(CAST(j1.Period AS VARCHAR(7)), 5, 2) AS INT) + 3 - 1) % 12, 
            DATEADD(YEAR, 
                    (CAST(SUBSTRING(CAST(j1.Period AS VARCHAR(7)), 5, 2) AS INT) + 3 - 1) / 12, 
                    CAST(SUBSTRING(CAST(j1.Period AS VARCHAR(7)), 1, 4) + '0101' AS DATE)
                   )
           ) AS FinDate
FROM 
    j1;
