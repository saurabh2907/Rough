DECLARE @CurrentMonth VARCHAR(7) = CONCAT_WS('/', YEAR(GETDATE()), MONTH(GETDATE()));
DECLARE @PreviousMonth VARCHAR(7) = 
    CASE 
        WHEN MONTH(GETDATE()) = 1 THEN CONCAT_WS('/', YEAR(GETDATE()) - 1, 12)
        ELSE CONCAT_WS('/', YEAR(GETDATE()), MONTH(GETDATE()) - 1)
    END;


UPDATE [FinDB].[dbo].[DailyPremIssued]
SET Name = CASE 
    WHEN [PREMIUM_AMT] = 0 THEN 'SINGLE PREMIUMS'
    WHEN [RATED_PREMIUM] / [PREMIUM_AMT] = 1 THEN 'FIRST YEAR PREMIUMS'
    ELSE 'SINGLE PREMIUMS'
END
WHERE (
    CONCAT_WS('/', LEFT([Accounting_Period], 4), CONVERT(INT, RIGHT([Accounting_Period], 3)) + 3) = @CurrentMonth
    OR CONCAT_WS('/', LEFT([Accounting_Period], 4), CONVERT(INT, RIGHT([Accounting_Period], 3)) + 3) = @PreviousMonth
  );



WHERE (
    CASE 
        WHEN CONVERT(INT, RIGHT([Accounting_Period], 2)) + 3 > 12 
            THEN CONCAT(CONVERT(INT, LEFT([Accounting_Period], 4)) + 1, '/', FORMAT((CONVERT(INT, RIGHT([Accounting_Period], 2)) + 3) % 12, '00'))
        ELSE CONCAT(LEFT([Accounting_Period], 4), '/', FORMAT(CONVERT(INT, RIGHT([Accounting_Period], 2)) + 3, '00'))
    END = @CurrentMonth
    OR 
    CASE 
        WHEN CONVERT(INT, RIGHT([Accounting_Period], 2)) + 3 > 12 
            THEN CONCAT(CONVERT(INT, LEFT([Accounting_Period], 4)) + 1, '/', FORMAT((CONVERT(INT, RIGHT([Accounting_Period], 2)) + 3) % 12, '00'))
        ELSE CONCAT(LEFT([Accounting_Period], 4), '/', FORMAT(CONVERT(INT, RIGHT([Accounting_Period], 2)) + 3, '00'))
    END = @PreviousMonth
);
