Volume_Delta_vs_Board = 
IF(ISINSCOPE(Grade[Clean_Grade]), ([.Board]*[Delta vs Board.])/100/12,
SUMX(VALUES(Grade[Clean_Grade]), ([.Board]*[Delta vs Board.])/100/12)
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
