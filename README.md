select distinct [Accounting Period], CONCAT(left([Accounting Period],4), '-', FORMAT(CAST(RIGHT([Accounting Period],2) as INT)+3,'00'), '-01') as [Month] from Premium_Dump
order by Month
