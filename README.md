import pandas as pd
import pyodbc

# Assuming df is your DataFrame
# Define your connection parameters
server = 'your_server'
database = 'your_database'
username = 'your_username'
password = 'your_password'

# Create the connection string
connection_string = f'DRIVER={{ODBC Driver 17 for SQL Server}};SERVER={server};DATABASE={database};UID={username};PWD={password}'

# Connect to SQL Server
cnxn = pyodbc.connect(connection_string)
cursor = cnxn.cursor()

# Iterate over the DataFrame rows and insert into SQL Server
for index, row in df.iterrows():
    cursor.execute("""
        INSERT INTO FinDB.DBO.Gross_Margin1 
        (SPCODE, PROD_CODE, AG_BRANCHCODE, AGE_AT_ENTRY, PRODUCT_ID, 
        POL_TERM_Y, PREM_PAYBL_M, PREM_FREQ, MTHS_TO_SALE, START_A_PREM, 
        START_DPRM_A, START_PVFP_A, START_S_PREM, START_DTRANA, LOB, VNB, ANP, 
        Month, DEFER_PER_Y, [LIFE/ROC], VARIANT, PARTNER_NAME, VERTICAL_NAME_MIS, POL_NUMBER) 
        VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
    """, 
    row['SPCODE'], row['PROD_CODE'], row['AG_BRANCHCODE'], row['AGE_AT_ENTRY'], row['PRODUCT_ID'], 
    row['POL_TERM_Y'], row['PREM_PAYBL_M'], row['PREM_FREQ'], row['MTHS_TO_SALE'], row['START_A_PREM'], 
    row['START_DPRM_A'], row['START_PVFP_A'], row['START_S_PREM'], row['START_DTRANA'], row['LOB'], 
    row['VNB'], row['ANP'], row['Month'], row['DEFER_PER_Y'], row['LIFE/ROC'], row['VARIANT'], 
    row['PARTNER_NAME'], row['VERTICAL_NAME_MIS'], row['POL_NUMBER'])

# Commit the transaction
cnxn.commit()

# Close the cursor and connection
cursor.close()
cnxn.close()
