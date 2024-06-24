UPDATE [FinDB].[dbo].[Daily_Premium_Retail]
SET [Channel] = CASE WHEN [CHANNELS]  = 'P0ZZ' THEN 'INSTITUTIONAL BUSINESS' ELSE
				A.[Channel] from [FinDB].[dbo].[T2-Channels] A
				JOIN [FinDB].[dbo].[Daily_Premium_Retail] B
				ON A.[T code] = B.[CHANNELS]
				END
