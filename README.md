VAR numerator = [Yournumeratorcolumn]
VAR denominator = [Yourdenominatorcolumn]
VAR total = numerator + denominator
VAR numerator_perc = DIVIDE(numerator, total) * 100
VAR denominator_perc = DIVIDE(denominator, total) * 100
RETURN
    CONCATENATE(
        PERCENTAGE(numerator_perc, 0),
        ":",
        PERCENTAGE(denominator_perc, 0)
    )
