## Arable land and permanent pastures-grasslands change in declared area:

## Steps followed

### Data preparation

### Step 1:

 Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

### Step 2:

 Load data into Power BI Desktop, dataset is excel file about municipalities, 3 classifiers from database about plant codes, it’s groups and group names.

### Step 3:

 Removed 13 unnecessary columns from table ‘Deklaruotos naudmenos’, source.name, municipalities and information about provided applications and declared area of other groups, except general number of declared area.

### Step 4:

 Wrote a DAX to merge year and group number so I could relate plant groups and plant group’s names.

	DAX was written for each table ‘Paseliu grupes’ and ‘Paseliu grupiu pavadinimai’:
    Grupe ir metai = 'Paseliu grupes'[REMIAMA_GRUPE]&'Paseliu grupes'[METAI]

### Step 5: 

Made relationships between data array table, municipalities table and classifiers.

### Step 6:

 Since arable land consists of 4 groups of plants wrote a DAX to SUM declared area of these groups:

	DAX was written:
    Ariamoji zeme IN = CALCULATE(SUM('Deklaruotos naudmenos'[BENDRAS_PLOTAS]),'Paseliu grupes'[REMIAMA_GRUPE] IN {1,2,3,4})

Permanent pastures-grasslands (5 years and more), natural grasslands, wetlands consists of group 6 plant codes and 2 plant codes from group 7.

	DAX was written:
    DGP = ROUND(CALCULATE(SUM('Deklaruotos naudmenos'[BENDRAS_PLOTAS]),'Paseliu grupes'[REMIAMA_GRUPE] IN {6}) + CALCULATE(SUM('Deklaruotos naudmenos'[BENDRAS_PLOTAS]),'Paselius klasifikatorius'[KODAS] IN {"MNN", "5PT-3"}),2)

Pastures or grasslands up to 5 years consists of group 4 plant codes.

	DAX was written:
    Pievos iki 5 metu = ROUND(CALCULATE(SUM('Deklaruotos naudmenos'[BENDRAS_PLOTAS]),'Paseliu grupes'[REMIAMA_GRUPE] IN {4}),2)

### Data visualization

### Step 1: 

For data visualization about arable took clustered column chart and line chart. 

### Step 2: 

Clustered column chart -> set font to arial, title size to 13, Y-axis and data labels values display units set to none, made black background and white text for tooltips.

### Step 3: 

Added text box with a note about arable land and permanent pastures-grasslands (5 years and more), natural grasslands, wetlands composition.

### Step 4:

 Line chart -> set font to arial, title size to 13, Y-axis and data labels values display units set to none, made black background and white text for tooltips. Set background for data labels and changed colors for each group.

### Step 5: 

Set font to arial, title size 13 as agreed in our company, made background for data labels and set different colors, set range for Y-axis, display units to none for data label’s values and for Y-axis values.

### Step 6:

 Set custom format to ### ### ##0.00 for column with information about declared area.

## Insights

### 1 page report was created. 

### Report was moved to Power BI service and published to web so I could use iFrame in visme environment. 

### It visualizes 10 years comparison of declared area of arable land and permanent pastures-grasslands (5 years and more), natural grasslands, wetlands.

### It visualizes 10 years comparison of declared area of permanent pastures-grasslands (5 years and more), natural grasslands, wetlands and pastures or grasslands up to 5 years.


