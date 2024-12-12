
## Change in provided applications and declared area in 2015-2024

## Steps followed

### Data preparation

### Step 1: 

Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

### Step 2:

 Load data into Power BI Desktop, dataset is excel file about municipalities.

### Step 3: 

Removed unnecessary column with about csv file and referenced table ‘Paraiskos ir plotas’. One more table ‘Paraiskos ir plotas 2024’ was created.

### Step 4:

 Wrote a dax to count rows with year from 2015 to 2023.

	DAX was written: 
    Countrows = COUNTROWS(FILTER('Paraiskos ir plotas', 'Paraiskos ir plotas'[METAI] IN {2015,2016,2017,2018,2019,2020,2021,2022,2023}))

Removed 4243 top rows from table ‘Paraiskos ir plotas 2024’, so I would have table only with year 2024.

### Step 5:

 Removed unnecessary columns from table ‘Paraiskos ir plotas’, because I needed information only about general number of applications and declared area and declarations through e-government portal.

### Step 6: 

Made relationships between data array tables and municipalities table. 

### Data visualization

### Step 1:

 For data visualization from table ‘Paraiskos ir plotas 2024’ took matrix. 

### Step 2:

 Set font to arial, set background for headers, removed horizontal gridlines, set background for alternate value color.

### Step 3:

 For data visualization from table ‘Paraiskos ir plotas’, took line and stacked column charts, since meanings of values were different and also number.

### Step 4:

 Set font to arial, title size 13 as agreed in our company, made background for data labels and set different colors, set range for Y-axis, display units to none for data label’s values and for Y-axis values.
### Step 5:

 Set custom format to ### ### ##0. for all columns with information about number of applications and ### ### ##0.00 with information about declared area.

## Insights

### 1 page report was created. 

### Report was moved to Power BI service and published to web so I could use iFrame in visme environment. 

### It visualizes 10 years data about provided general number of applications and declared area and provided applications and declared area using e-gov portal. Also you can find statistics of 2024 about provided applications and declared area of 6 different groups.



