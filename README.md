WITH CTE AS (
    SELECT 
        [AllowanceDate], 
        [Prd ID],
        [AG_BRANCHCODE],
        [Product Code],
        [POL_TERM_Y],
        [PREM_FREQ],
        [PREM_PAYBL_M],
        [LOB],
        [NEW_SPCODE],
        [Channel_Codes],
        [Partner_Codes],
        [Retail_grp],
        SUM([BASECOM_PAID]) AS amt,
        LAG(SUM([BASECOM_PAID])) OVER (
            PARTITION BY 
                [Prd ID],
                [AG_BRANCHCODE],
                [Product Code],
                [POL_TERM_Y],
                [PREM_FREQ],
                [PREM_PAYBL_M],
                [LOB],
                [NEW_SPCODE],
                [Channel_Codes],
                [Partner_Codes],
                [Retail_grp]
            ORDER BY [AllowanceDate]
        ) AS prev_amt
    FROM Allowances
    GROUP BY
        [AllowanceDate],
        [Prd ID],
        [AG_BRANCHCODE],
        [Product Code],
        [POL_TERM_Y],
        [PREM_FREQ],
        [PREM_PAYBL_M],
        [LOB],
        [NEW_SPCODE],
        [Channel_Codes],
        [Partner_Codes],
        [Retail_grp]
)
SELECT 
    [AllowanceDate],
    [Prd ID],
    [AG_BRANCHCODE],
    [Product Code],
    [POL_TERM_Y],
    [PREM_FREQ],
    [PREM_PAYBL_M],
    [LOB],
    [NEW_SPCODE],
    [Channel_Codes],
    [Partner_Codes],
    [Retail_grp],
    amt, 
    prev_amt, 
    amt - prev_amt AS diff
FROM CTE;
