Total Availability (A) = 
// VAR a = CALCULATE(SELECTEDMEASURE(),Net_Margin[Attribute] = "TotalAllowance-COA+SREPR+SREPO") 
VAR b = CALCULATE(SELECTEDMEASURE(),Net_Margin[Attribute] = "VNB")
// VAR c=a+b
RETURN
b
