Row Level:- 

NB excl. Fund Based = 

CALCULATE(SELECTEDMEASURE(), Expense[IRDA GROUPING] IN {"FIRST YEAR PREMIUMS", "SINGLE PREMIUMS"})
-
CALCULATE(SELECTEDMEASURE(), Expense[Product_Nature] = "FUND" , Expense[IRDA GROUPING] IN {"FIRST YEAR PREMIUMS", "SINGLE PREMIUMS", "RENEWAL PREMIUMS"})

Column Level:-

Ach% MBR = 
VAR Actual = CALCULATE(SELECTEDMEASURE(),DATESMTD(DimDate[Date]), Expense[LedgerFull]= "Actual")

VAR AOP = CALCULATE(SELECTEDMEASURE(), DATESMTD(DimDate[Date]), Expense[LedgerFull]= "MBR")
RETURN
DIVIDE(Actual,AOP,0)

I am getting wrong Ach% MBR value NB excl. Fund Based row level calculation. Correct the issue
