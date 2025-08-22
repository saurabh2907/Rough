Volume_Delta_vs_Board = 
VAR CurrentContext = CALCULATE([.Board][Delta vs Board.], ALLSELECTED('Date'))
RETURN
IF(
    ISINSCOPE(Grade[Clean_Grade]),
    CurrentContext / 100 / 12,
    SUMX(
        VALUES(Grade[Clean_Grade]),
        CALCULATE(CurrentContext / 100 / 12, ALLEXCEPT(Grade, Grade[Clean_Grade]))
    )
)



VAR userEmail = USERPRINCIPALNAME()
RETURN
    COUNTROWS(
        FILTER(
            'AccessMap',
            'AccessMap'[Email] = userEmail &&
            (
                ('AccessMap'[GM] = 'Sales'[GM] || ISBLANK('AccessMap'[GM])) &&
                ('AccessMap'[Zone] = 'Sales'[Zone] || ISBLANK('AccessMap'[Zone])) &&
                ('AccessMap'[Vertical] = 'Sales'[Vertical] || ISBLANK('AccessMap'[Vertical])) &&
                ('AccessMap'[SGM] = 'Sales'[SGM] || ISBLANK('AccessMap'[SGM]))
            )
        )
    ) > 0
