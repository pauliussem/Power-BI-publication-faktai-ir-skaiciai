## Change in crops declared area in 2023-2024 (yoy)

## Steps followed

### Data preparation

### Step 1: 

Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

### Step 2: 

Load data into Power BI Desktop, dataset is excel file plants classifier. 

### Step 3: 

Removed unnecessary columns about provided applications and declared area. Left only general information about declared area.

### Step 4: 

Wrote a DAX to count rows with year from 2015 to 2023.

	DAX was written:
    countrows = COUNTROWS(FILTER('Deklaruotas plotas', 'Deklaruotas plotas'[METAI] in {2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022}))

Removed 174848 top rows from table ‘Deklaruotas plotas and left information about 2023 and 2024.

### Step 5: 

According to plant code, picked plant ID’s from year 2023 and 2024 from database and prepared to use it in Power BI.

	DAXs were written: 
    =A2&", " (for all IDs in a column) 
    =CONCAT(B2:B17) 

![6_1](https://github.com/user-attachments/assets/51bf75a2-718c-45a9-8661-4cda724b4354)

### Step 6: 

Created new table according to ‘Deklaruotos naudmenos’.

	DAX was written:
    2024 deklaruotas plotas = CALCULATETABLE('Deklaruotas plotas', 'Deklaruotas plotas'[METAI] IN {2024}, 'Deklaruotas plotas'[KULTUROS_ID] IN {403, 410, 405, 411, 404, 450, 662, 412, 408, 600, 413, 402, 743, 409, 415, 733})

### Step 7:

Created new table with necessary names of plants, according to plants classifier.

	DAX was written:
    Atrinktas paseliu kl = CALCULATETABLE('Paseliu klasifikatorius', 'Paseliu klasifikatorius'[ID] IN {403, 410, 405, 411, 404, 450, 662, 412, 408, 600, 413, 402, 743, 409, 415, 733})

### Step 8: 

Since year were provided as whole number, created new column and set data type as “Date”.

	DAX was written:
    Metai data = '2023 2024 plotas'[METAI]&"/01"&"/01"

### Step 9: 

Created new measure to calculate last year’s declared area, which I am going to use to calculate year over year growth.

	DAX was written:
    Praeiti metai = CALCULATE(SUM('2023 2024 plotas'[BENDRAS_PLOTAS]), DATEADD('2023 2024 plotas'[Metai data].[Date], -1, YEAR))

### Step 10: 

Calculated YoY growth and set format to “Percentage”.

	DAX was written:
    Yoy augimas = ROUND(DIVIDE(SUM('2024 deklaruotas plotas'[BENDRAS_PLOTAS])-[Praeiti metai], [Praeiti metai]),2)

### Step 11: 

Created new measure, which will be used to store names of plants over bars later.

	DAX was written:
    Placeholder = 0

### Data visualization

### Step 1: 

For data visualization took clustered bar charts. 

### Step 2:

For X-axis imported information about declared area and measure [placeholder].

### Step 3: 

Set data labels on. Applied settings to [placeholder]. Turned off values and in detail > data field added names of plants from ‘Atrinktas paseliu kl’[PAVADINIMAS].

![6_2](https://github.com/user-attachments/assets/d0b897e6-0a5f-4b07-820d-17266fafb997)


### Step 4: 

Turned off values of Y-axis.

### Step 5: 

Other chart was for declared area change. Picked measure [Yoy augimas].

### Step 6: 

Set range, conditional bar color. Green -> growth, red > decrease. Turned on data labels and set conditional detail label colors.

![6_3](https://github.com/user-attachments/assets/4856f1cc-a4ed-4b6d-bb35-25e5eaa0b1c8)


## Insights

### 1 page report was created. 
### Report was moved to Power BI service and published to web so I could use iFrame in visme environment. 
### It visualizes declared area of picked plants in 2024 and change of declared area compared to 2023.
