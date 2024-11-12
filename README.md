import pandas as pd
from sqlalchemy import create_engine

# Load data from CSV file into DataFrame
# Example: SMS_Dump = pd.read_csv("path_to_csv_file.csv")

# Database connection details
server = 'L1SRW2FND01'
database = 'FinDB'
uid = 'mis_finance'
pwd = 'Misfinancelife@321'

# Create an SQLAlchemy engine
engine = create_engine(f'mssql+pyodbc://{uid}:{pwd}@{server}/{database}?driver=ODBC+Driver+17+for+SQL+Server')

# Insert the DataFrame into SQL Server
SMS_Dump.to_sql(
    '382000_bajaj_allianz_ccm_groupops_trans',  # table name
    con=engine,
    schema='dbo',
    if_exists='append',  # appends to the existing table
    index=False,  # do not write DataFrame index as a column
    chunksize=1000  # number of rows to insert at a time
)
