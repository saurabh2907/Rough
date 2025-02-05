NOP_Count = 
VAR PolicyTable =
    ADDCOLUMNS(
        SUMMARIZE(Dump_FTM, Dump_FTM[POLICY_REF]),
        "PremAmount",
            CALCULATE(
                SUM(Dump_FTM[PREM_AMOUNT])
            ),
        "AdjDateFormatted",
            FORMAT(MAX(Dump_FTM[ADJ_DATE]), "MM-YYYY"),
        "AccountingDateFormatted",
            FORMAT(MAX(Dump_FTM[ACCOUNTING_DATE]), "MM-YYYY")
    )

RETURN
    COUNTROWS(
        FILTER(
            PolicyTable,
            [AdjDateFormatted] = [AccountingDateFormatted] &&
            [PremAmount] > 0
        )
    )
