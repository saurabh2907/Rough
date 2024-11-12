BULK INSERT dbo.382000_bajaj_allianz_ccm_groupops_trans
FROM 'path_to_csv_file.csv'
WITH (
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '\n',
    FIRSTROW = 2  -- Skip header row
)
