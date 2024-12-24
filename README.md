Color_Ach% MBR = 
VAR a = ISSELECTEDMEASURE([Ach% AOP_Amt_MTD],[Ach% AOP_Amt_YTD],[Ach% Board_Amt_MTD],[Ach% Board_Amt_YTD],[Ach% MBR AOP_Amt_MTD],[Ach% MBR AOP_Amt_YTD])
RETURN
SWITCH(TRUE(),
 a < 0.90, "#FFC7CE",
a > 0.99, "#C6EFCE",
a >= 0.90 && a <= 0.99, "#FFEB9C")
