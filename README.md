## Change in arable land declared area by municipalities (choropleth map)

### NOTE: Since similar steps were applied for all 5 maps information provided only about this map.

## Steps followed


### Data preparation

### Step 1:

 Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

### Step 2: 

Load data into Power BI Desktop, dataset is excel file about municipalities, 3 classifiers from database about plant codes, it’s groups and group names.
### Step 3: 

Wrote a DAX to count rows with year from 2015 to 2022.

	DAX was written:
    Countrows = COUNTROWS(FILTER('Deklaruotos naudmenos', 'Deklaruotos naudmenos'[METAI] IN {2015,2016,2017,2018,2019,2020,2021,2022}))

### Step 4: 

174848 top rows and unnecessary columns from table ‘Deklaruotos naudmenos’ were removed.

### Step 5: 

Wrote a DAX to merge year and group number so I could relate plant groups and plant group’s names:

	DAX was written for each table ‘Paseliu grupes’ and ‘Paseliu grupiu pavadinimai’:
    Grupe ir metai = 'Paseliu grupes'[REMIAMA_GRUPE]&'Paseliu grupes'[METAI]

### Step 6: 

Made relationships between data array table, municipalities table and classifiers.

### Step 7: 

Since arable land consists of 4 groups of plants wrote a DAX to SUM declared area of these groups and created new table according to ‘Deklaruotos naudmenos’

	DAX was written:
    Ariamoji 2023 ir 2024 = CALCULATETABLE('Deklaruotos naudmenos', FILTER('Paseliu grupes','Paseliu grupes'[REMIAMA_GRUPE] IN {1,2,3,4}), FILTER('Deklaruotos naudmenos', 'Deklaruotos naudmenos'[METAI] IN {2023, 2024}))
### Step 8: 

Summed up declared area of years 2023 and 2024 each.

	DAXs were written:
    SUM ariamoji zeme 2023 = CALCULATE(SUM('Ariamoji 2023 ir 2024'[BENDRAS_PLOTAS]), 'Ariamoji 2023 ir 2024'[METAI] IN {2023})
    SUM ariamoji zeme 2024 = CALCULATE(SUM('Ariamoji 2023 ir 2024'[BENDRAS_PLOTAS]), 'Ariamoji 2023 ir 2024'[METAI] IN {2024})

### Step 9:

Calculated difference between declared area of 2023 and 2024.

	DAX was written:
    Deklaruoto ploto pokytis, ha = [SUM ariamoji zeme 2024]-[SUM ariamoji zeme 2023]
### Step 10: 

Since regular number formatting doesn’t work as I would expect with minus values (if I add space after thousands, space appears between value and minus sign which is above -1000), so I wrote a DAX to format [Deklaruoto ploto pokytis, ha].

	DAX was written:
    Formated ploto pokytis = IF([Deklaruoto ploto pokytis, ha] < 0,
    VAR pokytis = 
    FORMAT([Deklaruoto ploto pokytis, ha], "#,0.00")
    RETURN
    SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(pokytis, ".", "@"), ",", " "), "@", ","),
    VAR pokytis2 =
    FORMAT([Deklaruoto ploto pokytis, ha], "#,0.00")
    RETURN
    SUBSTITUTE(SUBSTITUTE(pokytis2,",", " "),".",","))

### Step 11: 

Since I didn’t wanted a difference between first two cards of SUM values and card with difference value if end-user is watching this dashboard from different region, changed format of [SUM ariamoji zeme 2023] and [SUM ariamoji zeme 2023].

![3_1](https://github.com/user-attachments/assets/0c574b50-0bfd-4eba-b271-c70e0b8112b8)


	DAXs were written:
    2023 SUM F = IF([SUM ariamoji zeme 2023] > 0,
    VAR pokytis = 
    FORMAT([SUM ariamoji zeme 2023], "#,0.00")
    RETURN
    SUBSTITUTE(SUBSTITUTE(pokytis, ",", " "),".",","), "-")
    **************
    2024 SUM F = IF([SUM ariamoji zeme 2024] > 0,
    VAR pokytis = 
    FORMAT([SUM ariamoji zeme 2024], "#,0.00")
    RETURN
    SUBSTITUTE(SUBSTITUTE(pokytis, ",", " "),".",","), "-")

### Step 12: 

Since in shape map I couldn’t use measure as color saturation, had to find a way to find difference between each municipality. Created matrix with SUM values of declared area for 2023 and 2024 and exported data.

![3_2](https://github.com/user-attachments/assets/0fd26fe3-d81f-48c7-a4da-203ccfba3c1d)

### Step 13: 

Using excel, calculated difference between years and added table to power BI.

### Step 14: 

Since FORMAT makes numbers to strings, used regular formatting (# ##0.00;-##0.00) in power BI and unfortunately values bellow -1000 will appear without space after 3 digits.

### Step 15:  

Created Legend table, with 6 different sections and applied number for each section, so I could relate it with ‘Ariamoji pokytis’ table.

    DAX was written:
    Legend table = SELECTCOLUMNS({("#F7B839", "-1500 – -1000", 1, 1),
    ("#C7A75A", "-1000 – -500", 2, 2),
    ("#AE9C73", "-500 – 0", 3, 3),
    ("#746B4E", "0 – 500", 4, 4),
    ("#5D5745", "500 – 1000", 5, 5),
    ("#B6B9BD", "Duomenų nėra", 6, {blank()})},
        "Color",[Value1], "Riba", [Value2], "eile", [Value3], "tvarka", [Value4])

### Step 16:  

Created column in table ‘Ariamoji pokytis’ regarding difference of declared area of each municipality and assigned number of each section.

	DAX was written:
    Pogrupis = 
    IF('Ariamoji pokytis'[Pokytis] < -1000, 1, 
    IF('Ariamoji pokytis'[Pokytis] < -500, 2, 
    IF('Ariamoji pokytis'[Pokytis] < 0, 3, 
    IF('Ariamoji pokytis'[Pokytis] < 500, 4,
    IF('Ariamoji pokytis'[Pokytis] < 1000, 5,
    IF('Ariamoji pokytis'[Pokytis] = {BLANK()}, 6, 0))))))

### Step 17:  

Made relationships between all tables.

![3_3](https://github.com/user-attachments/assets/8e440a04-793e-4789-94db-36536a39b5f6)


### Step 18:  

Wrote a DAX, so in card would appear “Selected municipalities” in case if two or more municipalities are selected.

![3_4](https://github.com/user-attachments/assets/73a07e53-c523-429a-b1af-52b660fc5a55)


    DAX was written:
    Visos savivaldybes = IF(HASONEVALUE('Savivaldybiu ID'[SAV_PAVADINIMAS]),SELECTEDVALUE('Savivaldybiu ID'[SAV_PAVADINIMAS]),"Pasirinktose savivaldybėse")

### Data visualization

### Step 1: 

For data visualization of declared area change took shape map, 4 cards for general information and table for legend.

### Step 2: 

Added prepared TopoJSON file about Lithuania’s municipalities. 

### Step 3: 

For color saturation took change of declared area from table ‘Ariamoji pokytis’.

### Step 4: 

Took min and max values, divided from 5 and counted 5 equal parts and set minimum and maximum values and set gradient colors.

![3_5](https://github.com/user-attachments/assets/2ff9d5db-bf68-4183-b421-7dce15382eba)



### Step 5: 

In table added color and riba columns from table ‘Legend table’.

### Step 6: 

With conditional formatting set gradient colors of color column same as in shape map for background and text.

### Step 7: 

Since these tables were related from the past, by pressing any section you can filter municipalities, which belongs to assigned section.

![3_6](https://github.com/user-attachments/assets/c8ec2112-e236-46ac-9a44-e75f16e9ccd1)


### Step 8: 

Used cards to provide general information about selected municipalities, declared area in 2023 and 2024 and declared area difference.

## Insights

### 1 page report was created. 

### Report was moved to Power BI service and published to web so I could use iFrame in visme environment. 

### It visualizes change of declared area of each municipality by comparing declared area in 2023 and 2024.
