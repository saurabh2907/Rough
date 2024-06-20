WITH CTE AS (
select [[AllowanceDate]]], [Prd ID]
	,[AG_BRANCHCODE]
	,[Product Code]
	,[POL_TERM_Y]
    ,[PREM_FREQ]
    ,[PREM_PAYBL_M]
	,[LOB]
	,[NEW_SPCODE]
    ,[Channel_Codes]
    ,[Partner_Codes]
    ,[Retail_grp],

sum([BASECOM_PAID]) as amt, 
lag(sum([BASECOM_PAID])) over(
order by [[AllowanceDate]]]) as prev_amt

from Allowances
group by
	 [[AllowanceDate]]]
	,[Prd ID]
	,[AG_BRANCHCODE]
	,[Product Code]
	,[POL_TERM_Y]
    ,[PREM_FREQ]
    ,[PREM_PAYBL_M]
	,[LOB]
	,[NEW_SPCODE]
    ,[Channel_Codes]
    ,[Partner_Codes]
    ,[Retail_grp]
)

	select [[AllowanceDate]]],
[Prd ID]
	,[AG_BRANCHCODE]
	,[Product Code]
	,[POL_TERM_Y]
    ,[PREM_FREQ]
    ,[PREM_PAYBL_M]
	,[LOB]
	,[NEW_SPCODE]
    ,[Channel_Codes]
    ,[Partner_Codes]
    ,[Retail_grp], amt, prev_amt, amt - prev_amt as diff
	from CTE
