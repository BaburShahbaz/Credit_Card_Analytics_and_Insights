## **DAX Queries**





**---  For Age Group**



AgeGroup = SWITCH(

&nbsp;    TRUE(),

&nbsp;    'public cust\_detail'\[customer\_age] < 30,"20-30",

&nbsp;    'public cust\_detail'\[customer\_age] < 30,"20-30",

&nbsp;    'public cust\_detail'\[customer\_age] >= 30 \&\& 'public cust\_detail'\[customer\_age] < 40,"30-40",

&nbsp;    'public cust\_detail'\[customer\_age] >= 40 \&\& 'public cust\_detail'\[customer\_age] < 50,"40-50",

&nbsp;    'public cust\_detail'\[customer\_age] >= 50 \&\& 'public cust\_detail'\[customer\_age] < 60,"50-60",

&nbsp;    'public cust\_detail'\[customer\_age] >= 60, "60+",

&nbsp;    "unknown"

)





**--- For Income Group**



IncomeGroup = SWITCH(

&nbsp;   TRUE(),

&nbsp;   'public cust\_detail'\[income] < 35000, "Low",

&nbsp;   'public cust\_detail'\[income] >= 35000 \&\& 'public cust\_detail'\[income] < 70000, "Medium",

&nbsp;   'public cust\_detail'\[income] >= 70000, "High",

&nbsp;   "unknown"

)





**--- for revenue**



revenue = 'public cc\_detail'\[annual\_fees] + 'public cc\_detail'\[total\_trans\_amt] + 'public cc\_detail'\[interest\_earned] 





**--- for week\_num2**



week\_num2 = WEEKNUM('public cc\_detail'\[week\_start\_date]) 







## **Adding Measures** 



**--- For current week revenue**



current\_week\_revenue = CALCULATE(

&nbsp;   SUM('public cc\_detail'\[revenue]),

&nbsp;   FILTER(

&nbsp;       ALL('public cc\_detail'),

&nbsp;       'public cc\_detail'\[week\_num2] = MAX('public cc\_detail'\[week\_num2]))

)





**--- For previous week revenue**



previous\_week\_revenue = CALCULATE(

&nbsp;   SUM('public cc\_detail'\[revenue]),

&nbsp;   FILTER(

&nbsp;       ALL('public cc\_detail'),

&nbsp;       'public cc\_detail'\[week\_num2] = MAX('public cc\_detail'\[week\_num2])-1

&nbsp;       )

&nbsp;   )







**--- For weak revenue**



weak\_revenue = DIVIDE((\[current\_week\_revenue]-\[previous\_week\_revenue]),\[previous\_week\_revenue])













