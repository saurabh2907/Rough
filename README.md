CREATE PROCEDURE ImportXLSB 
    @FilePath NVARCHAR(500), 
    @TableName NVARCHAR(100)
AS
BEGIN
    DECLARE @SQL NVARCHAR(MAX)
    
    -- Specify the columns from the Excel file
    SET @SQL = 'INSERT INTO ' + @TableName + ' (Column1, Column2, Column3, Column4, Column5) ' + 
               'SELECT Column1, Column2, Column3, Column4, Column5 ' + 
               'FROM OPENROWSET(''Microsoft.ACE.OLEDB.12.0'', ''Excel 12.0 Xml; HDR=YES; Database=' + @FilePath + ''', [Sheet1$])'
    
    EXEC sp_executesql @SQL
END;
