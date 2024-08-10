DEFINE
	VAR __DS0FilterTable = 
		TREATAS({"MAY"}, 'DimDate'[Month Name])

	VAR __DS0FilterTable2 = 
		TREATAS({"FY-25"}, 'DimDate'[FY Year])

	VAR __DS0Core = 
		SUMMARIZECOLUMNS(
			'Ratio'[Calculation group column],
			'Ratio'[Ordinal],
			'Premium Ledger'[Calculation group column],
			'Premium Ledger'[Ordinal],
			__DS0FilterTable,
			__DS0FilterTable2,
			"Amounts", 'Expense'[Amounts],
			"v_Amounts_FormatString", IGNORE('Expense'[_Amounts FormatString]),
			"Color_Ach_", IGNORE('Premium Ledger'[Color_Ach%]),
			"v_Color_Ach__FormatString", IGNORE('Premium Ledger'[_Color_Ach% FormatString]),
			"Color_Growth_", IGNORE('Premium Ledger'[Color_Growth%]),
			"v_Color_Growth__FormatString", IGNORE('Premium Ledger'[_Color_Growth% FormatString])
		)

	VAR __DS0PrimaryWindowed = 
		TOPN(
			101,
			SUMMARIZE(__DS0Core, 'Ratio'[Calculation group column], 'Ratio'[Ordinal]),
			'Ratio'[Ordinal],
			1,
			'Ratio'[Calculation group column],
			1
		)

	VAR __DS0SecondaryBase = 
		SUMMARIZE(__DS0Core, 'Premium Ledger'[Calculation group column], 'Premium Ledger'[Ordinal])

	VAR __DS0Secondary = 
		TOPN(
			102,
			__DS0SecondaryBase,
			'Premium Ledger'[Ordinal],
			1,
			'Premium Ledger'[Calculation group column],
			1
		)

	VAR __DS0BodyLimited = 
		NATURALLEFTOUTERJOIN(
			__DS0PrimaryWindowed,
			SUBSTITUTEWITHINDEX(
				__DS0Core,
				"ColumnIndex",
				__DS0Secondary,
				'Premium Ledger'[Ordinal],
				ASC,
				'Premium Ledger'[Calculation group column],
				ASC
			)
		)

EVALUATE
	__DS0Secondary

ORDER BY
	'Premium Ledger'[Ordinal], 'Premium Ledger'[Calculation group column]

EVALUATE
	__DS0BodyLimited

ORDER BY
	'Ratio'[Ordinal], 'Ratio'[Calculation group column], [ColumnIndex]
