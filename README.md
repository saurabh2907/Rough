CREATE PROCEDURE ImportXLSB 
    @FilePath NVARCHAR(500), 
    @TableName NVARCHAR(100)
AS
BEGIN
    DECLARE @SQL NVARCHAR(MAX)
    
    -- Specify the columns from the Excel file
    SET @SQL = 'INSERT INTO ' + @TableName + ' ([SPCODE]
      ,[PROD_CODE]
      ,[AG_BRANCHCODE]
      ,[AGE_AT_ENTRY]
      ,[PRODUCT_ID]
      ,[POL_TERM_Y]
      ,[PREM_PAYBL_M]
      ,[PREM_FREQ]
      ,[MTHS_TO_SALE]
      ,[START_A_PREM]
      ,[START_DPRM_A]
      ,[START_PVFP_A]
      ,[START_S_PREM]
      ,[START_DTRANA]
      ,[LOB]
      ,[VNB]
      ,[ANP]
      ,[Month]
      ,[DEFER_PER_Y]
      ,[LIFE/ROC]
      ,[VARIANT]
      ,[PARTNER_NAME]
      ,[VERTICAL_NAME_MIS]
      ,[POL_NUMBER]) ' + 

               'SELECT [SPCODE]
      ,[PROD_CODE]
      ,[AG_BRANCHCODE]
      ,[AGE_AT_ENTRY]
      ,[PRODUCT_ID]
      ,[POL_TERM_Y]
      ,[PREM_PAYBL_M]
      ,[PREM_FREQ]
      ,[MTHS_TO_SALE]
      ,[START_A_PREM]
      ,[START_DPRM_A]
      ,[START_PVFP_A]
      ,[START_S_PREM]
      ,[START_DTRANA]
      ,[LOB]
      ,[VNB]
      ,[ANP]
      ,[Month]
      ,[DEFER_PER_Y]
      ,[LIFE/ROC]
      ,[VARIANT]
      ,[PARTNER_NAME]
      ,[VERTICAL_NAME_MIS]
      ,[POL_NUMBER] ' + 
               'FROM OPENROWSET(''Microsoft.ACE.OLEDB.12.0'', ''Excel 12.0 Xml; HDR=YES; Database=' + @FilePath + ''', [Sheet1$])'
    
    EXEC sp_executesql @SQL
END;
