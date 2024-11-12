%%time

import pyodbc
import pandas as pd
# insert data from csv file into dataframe.
# working directory for csv file: type "pwd" in Azure Data Studio or Linux
# working directory in Windows c:\users\username
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
Driver= 'ODBC+Driver+16+for+SQL+Server'
Server = 'L1SRW2FND01'
database = 'FinDB'
UID = 'mis_finance'
PWD= 'Misfinancelife@321'

cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+Server+';DATABASE='+database+';UID='+UID+';PWD='+ PWD)
cursor = cnxn.cursor()
# Insert Dataframe into SQL Server:
# Prepare the SQL query with placeholders
sql_query = """
    INSERT INTO [FinDB].[DBO].[382000_bajaj_allianz_ccm_groupops_trans]
    (Delivery_DateTime, Publish_DateTime, Item_ID, KeyWord,
       Messege, Mobile_No, Delivery_Status, smsParts, Req_Id) 
    VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)
"""

# Create a list of tuples containing the DataFrame data
data_to_insert = [
    (row['Delivery_DateTime'], row['Publish_DateTime'], row['Item_ID'], 
                   row['KeyWord'], row['Messege'], row['Mobile_No'], row['Delivery_Status'], 
                   row['smsParts'], row['Req_Id'])
    for index, row in SMS_Dump.iterrows()
]

# Execute the SQL query using executemany
cursor.executemany(sql_query, data_to_insert)

# Commit the transaction
cnxn.commit()

# Close the cursor and connection
cursor.close()
cnxn.close()
