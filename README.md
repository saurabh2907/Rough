SELECT
    YourColumn,
    CASE
        WHEN CHARINDEX('Fre_', YourColumn) > 0 AND CHARINDEX('|', YourColumn, CHARINDEX('Fre_', YourColumn)) > CHARINDEX('Fre_', YourColumn) + 4
        THEN SUBSTRING(
            YourColumn,
            CHARINDEX('Fre_', YourColumn) + 4,
            CHARINDEX('|', YourColumn, CHARINDEX('Fre_', YourColumn)) - CHARINDEX('Fre_', YourColumn) - 4
        )
        ELSE NULL
    END AS ExtractedValue
FROM YourTable;
