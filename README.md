-- Create the table
CREATE TABLE YourTable (
    YourColumn VARCHAR(50)
);

-- Insert sample data
INSERT INTO YourTable (YourColumn) VALUES
('SP_Code-|Fre_12|PT_20|Age_'),
('SP_Code-|Fre_1|PT_99|Age_'),
('SP_Code-|Fre_123|PT_99|Age_'),
('SP_Code-|Fre_4|PT_99|Age_');

-- Extract the numeric value after 'Fre_' and before '|'
SELECT YourColumn,
       SUBSTRING(
           YourColumn,
           CHARINDEX('Fre_', YourColumn) + 4,
           CHARINDEX('|', YourColumn, CHARINDEX('Fre_', YourColumn)) - CHARINDEX('Fre_', YourColumn) - 4
       ) AS ExtractedValue
FROM YourTable;
