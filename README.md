%%time

import pyodbc
import pandas as pd

# Load data from CSV file into a DataFrame
# For example:
# SMS_Dump = pd.read_csv("path_to_csv_file.csv")

# Database connection details
Driver = 'ODBC Driver 16 for SQL Server'
Server = 
database =
UID =
PWD =

# Create the connection
cnxn = pyodbc.connect(
    f'DRIVER={Driver};SERVER={Server};DATABASE={database};UID={UID};PWD={PWD}'
)
cnxn.fast_executemany = True  # Enable fast_executemany for faster bulk inserts

cursor = cnxn.cursor()

# Prepare the SQL query with placeholders
sql_query = """
    INSERT INTO [FinDB].[DBO].[382000_bajaj_allianz_ccm_groupops_trans]
    (Delivery_DateTime, Publish_DateTime, Item_ID, KeyWord,
       Messege, Mobile_No, Delivery_Status, smsParts, Req_Id) 
    VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)
"""

# Convert the DataFrame to a list of tuples directly
data_to_insert = SMS_Dump[['Delivery_DateTime', 'Publish_DateTime', 'Item_ID', 
                           'KeyWord', 'Messege', 'Mobile_No', 'Delivery_Status', 
                           'smsParts', 'Req_Id']].values.tolist()

# Execute the SQL query using executemany
cursor.executemany(sql_query, data_to_insert)

# Commit the transaction
cnxn.commit()

# Close the cursor and connection
cursor.close()
cnxn.close()
