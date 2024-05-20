CREATE PROCEDURE ImportXLSB
@FilePath NVARCHAR(500),
@TableName NVARCHAR(100)

AS BEGIN

DECLARE @SQL NVARCHAR(MAX)

SET @SQL = '
INSERT INTO ' + @TableName + '
SELECT * FROM OPENROWSET(
''Microsoft.ACE.OLEDB.12.0'',
''Excel 12.0 Xml; HDR=YES; Database=' + @FilePath + ''',
[Sheet1$]
)'

EXEC sp_executesql @SQL
END;
