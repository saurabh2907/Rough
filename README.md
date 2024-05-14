def fund_nonfund(row):
    if row['Retail/Group'] == 'Group':
        if row['Vertical'] == 'CORPORATE BUSINESS' and row['Products'] != '245-Group Term Life New':
            return 'Fund'
        else:
            return 'Non Fund'
    else:
        return 'NA'
