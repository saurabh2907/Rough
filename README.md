delete from [FinDB].[dbo].[Daily_Premium] where Ledger = 'A' and CONCAT_WS('/',left([Accounting Period],4),CONVERT(INT, RIGHT([Accounting Period], 3))+3)
= concat_ws('/',year(getdate()),month(getdate()))



AllowanceData
Allowances
ANP_NOP_Dump
Booking_Frequency
Daily_PPT_Dump
Daily_Premium
Gross_Margin
PPT_Dump
Premium_Dump
Rider_Dump
SISO_Dump
Industry_CAGR
Industry_Data
Industry_Overall_financials
Manpower
IndustryAgency
![image](https://github.com/saurabh2907/Rough/assets/83023654/69ac7228-ef35-4804-b776-e201d4b1a606)
