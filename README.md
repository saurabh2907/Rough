Board AOP 4M = 
var max_dte = MAX(Premium_LRP_Dump[FinDate])
RETURN
CALCULATE(CALCULATE(SELECTEDMEASURE(),
DATESBETWEEN(Premium_LRP_Dump[FinDate],
DATE(YEAR(max_dte) - IF(MONTH(max_dte) < 4,1,0),4,1),
DATE(YEAR(max_dte) - IF(MONTH(max_dte) < 4,1,0),7,31)
)
),Premium_LRP_Dump[Ledger] = "B")
