## Declared area of crops in 2015-2024

## Steps followed

### Data preparation

### Step 1: 

Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

### Step 2: 

Load data into Power BI Desktop, dataset is excel file plants classifier.

### Step 3: 

Removed 13 unnecessary columns from table ‘Deklaruotos naudmenos’, source.name, municipalities and information about provided applications and declared area of other groups, except general number of declared area.

### Step 4: 

Created my own table about plant groups and assign ID for each group.

	DAX was written:
    Naudmenu grupes = {("Žieminiai kviečiai", 1),("Žieminiai rugiai", 2),
    ("Žieminiai kvietrugiai", 3), ("Žieminiai miežiai", 4), ("Vasariniai kviečiai", 5),
    ("Vasariniai (salykliniai) miežiai", 6), ("Vasariniai kvietrugiai", 7), ("Vasariniai rugiai", 8),
    ("Avižos", 9), ("Grikiai", 10), ("Kukurūzai", 11), ("Žirniai", 12), ("Pupos", 13),
    ("Vikiai (ir jų mišiniai)", 14),("Lubinai", 15), ("Žieminiai rapsai", 16),
    ("Vasariniai rapsai", 17), ("Cukriniai runkeliai", 18), ("Kanapės", 19), ("Linai", 20),
    ("Bulvės", 21), ("Daržovės", 22), ("Sodai ir uogynai", 23)}
### Step 5: 

Extracted relevant information from table ‘Deklaruotos naudmenos’  and created new table ‘Deklaruotos naudmenos pagal grupes’.

	DAX was written:
    Deklaruotos naudmenos pagal grupes = CALCULATETABLE('Deklaruotos naudmenos', 'Paselius klasifikatorius'[ID] IN  
    {444, 590, 591, 592, 593, 594, 596, 597, 598, 599, 601, 602, 603, 605, 606, 607, 608, 609, 610, 611, 617, 622, 627, 628, 
    630, 631, 636, 637, 639, 641, 643, 644, 646, 649, 650, 651, 652, 654, 698, 700, 714, 715, 717, 737, 738, 771, 409, 402,
    403, 404,405,406, 407, 662,408,410,411,412,413,414,415,665, 434,425, 426,447, 695, 	743,449,450,452, 453,600, 632,633,
    668, 669, 670, 671, 672, 673, 674, 675, 676, 677, 463, 464, 465, 466, 678, 679, 469, 470, 471, 472, 680, 681, 682, 683,
    684, 685, 616, 619, 620, 621, 624, 635, 653, 716, 722, 728, 739, 740, 746, 778, 779})

### Step 6: 

Created new column with assigned number for each group, depending on plant ID.

	DAX was written:
    Grupės = SWITCH(TRUE(), 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {444, 	590, 591, 592, 593, 594, 596, 597,
    598, 599, 601, 602, 603, 605, 606, 607, 608, 609, 610, 611, 617, 622, 627, 628, 630, 631, 636, 637, 639, 641, 643, 644,
    646, 649, 650, 651, 	652, 654, 698, 700, 714, 715, 717, 737, 738, 771}, 22, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {409},
    1, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {402}, 9, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {403},
    10, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {404}, 7, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {405},
    3, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {406, 407, 662}, 11, 'Deklaruotos 	naudmenos pagal grupes'[KULTUROS_ID] IN {408},
    5, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {410}, 6, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {411}, 4,
    'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN 	{412}, 17,'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {413}, 16,
    'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {414}, 8,'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {415}, 2,
    'Deklaruotos naudmenos pagal 	grupes'[KULTUROS_ID] IN {665, 434}, 19, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {425, 426}, 21,
    'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {447, 695, 743}, 13, 'Deklaruotos naudmenos pagal 	grupes'[KULTUROS_ID] IN {449}, 14,
    'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {450}, 12, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN 	{452, 453}, 15,
    'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {600, 632}, 18, 'Deklaruotos naudmenos pagal grupes'[KULTUROS_ID] IN {633}, 20,
    'Deklaruotos 	naudmenos pagal grupes'[KULTUROS_ID] IN {668, 669, 670, 671, 672, 673, 674, 675, 676, 677, 463, 464, 465,
    466, 678, 679, 469, 470, 471, 472, 680, 681, 682, 683, 684, 685, 	616, 619, 620, 621, 624, 635, 653, 716, 722, 728, 739,
    740, 746, 778, 779}, 23, 0)

### Step 7: 

Made relationship between tables ‘Deklaruotos naudmenos pagal grupes’ and ‘Naudmenu grupes’.


### Data visualization

### Step 1: 

Took matrix chart to visualize declared area of each group from 2015 to 2024.

### Step 2:

Set font to arial, set background for headers, removed horizontal gridlines, set background for alternate value color.

### Step 3: 

Set custom format to ### ### ##0.00 with information about declared area.

### Step 4: 

Created slicer with years in case end-user would like to compare different years easier.

## Insights

### 1 page report was created. 
### Report was moved to Power BI service and published to web so I could use iFrame in visme environment. 
### It visualizes 10 years statistics about declared area of each group of plants. 
