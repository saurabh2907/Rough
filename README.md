
Color_Ach% MBR = 
VAR Ach = 
    SWITCH(
        TRUE(),
        ISSELECTEDMEASURE([Ach% AOP_Amt_MTD]), [Ach% AOP_Amt_MTD],
        ISSELECTEDMEASURE([Ach% AOP_Amt_YTD]), [Ach% AOP_Amt_YTD],
        ISSELECTEDMEASURE([Ach% Board_Amt_MTD]), [Ach% Board_Amt_MTD],
        ISSELECTEDMEASURE([Ach% Board_Amt_YTD]), [Ach% Board_Amt_YTD],
        ISSELECTEDMEASURE([Ach% MBR AOP_Amt_MTD]), [Ach% MBR AOP_Amt_MTD],
        ISSELECTEDMEASURE([Ach% MBR AOP_Amt_YTD]), [Ach% MBR AOP_Amt_YTD]
    )
RETURN
SWITCH(
    TRUE(),
    Ach < 0.90, "#FFC7CE",
    Ach > 0.99, "#C6EFCE",
    Ach >= 0.90 && Ach <= 0.99, "#FFEB9C"
)
