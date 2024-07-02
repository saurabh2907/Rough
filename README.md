delete from [FinDB].[dbo].[Daily_Premium] where Ledger = 'A' and CONCAT_WS('/',left([Accounting Period],4),CONVERT(INT, RIGHT([Accounting Period], 3))+3)
= concat_ws('/',year(getdate()),month(getdate()))
