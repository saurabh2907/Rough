for index, row in df.iterrows():
     cursor.execute("INSERT INTO FinDB.DBO.Gross_Margin1
                    ('SPCODE', 'PROD_CODE', 'AG_BRANCHCODE', 'AGE_AT_ENTRY', 'PRODUCT_ID',
       'POL_TERM_Y', 'PREM_PAYBL_M', 'PREM_FREQ', 'MTHS_TO_SALE',
       'START_A_PREM', 'START_DPRM_A', 'START_PVFP_A', 'START_S_PREM',
       'START_DTRANA', 'LOB', 'VNB', 'ANP', 'Month', 'DEFER_PER_Y', 'LIFE/ROC',
       'VARIANT', 'PARTNER_NAME', 'VERTICAL_NAME_MIS', 'POL_NUMBER') 
        
        values(?,?,?,?)", row.DepartmentID, row.Name, row.GroupName)
cnxn.commit()
cursor.close()
