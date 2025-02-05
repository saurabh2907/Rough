NOP_Count = 
VAR PolicyTable =
    SUMMARIZE(
        Dump_FTM,
        Dump_FTM[POLICY_REF],
        "PremAmount", SUM(Dump_FTM[PREM_AMOUNT]),
        "MaxAdjDate", MAX(Dump_FTM[ADJ_DATE]),
        "MaxAccountingDate", MAX(Dump_FTM[ACCOUNTING_DATE])
    )
RETURN
COUNTROWS(
    FILTER(
        PolicyTable,
        MONTH([MaxAdjDate]) = MONTH([MaxAccountingDate]) &&
        YEAR([MaxAdjDate]) = YEAR([MaxAccountingDate]) &&
        [PremAmount] > 0
    )
)
