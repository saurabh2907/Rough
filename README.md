SELECT DISTINCT
    [Accounting Period],
    CONCAT(
        CASE 
            WHEN RIGHT([Accounting Period], 2) IN ('10', '11', '12') 
            THEN LEFT([Accounting Period], 4) + 1 
            ELSE LEFT([Accounting Period], 4) 
        END,
        '-',
        FORMAT(
            CASE 
                WHEN RIGHT([Accounting Period], 2) IN ('10', '11', '12') 
                THEN RIGHT([Accounting Period], 2) - 9 
                ELSE RIGHT([Accounting Period], 2) + 3 
            END,
            '00'
        ),
        '-01'
    ) AS [Month]
FROM 
    Premium_Dump
ORDER BY 
    [Month];
