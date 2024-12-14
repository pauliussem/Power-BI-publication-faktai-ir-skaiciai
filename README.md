## Publication "Faktai ir skaičiai"



Publication "Faktai ir skaičiai" is published one time per year. It consists of different statistics from different departments.

I had to prepare statistics about provided applications and declared area of crops to claim a support from EU funds.

## Steps followed

### Data preparation

Prepared data array for all dashboards. Had to extract 2 different arrays. First for general data about provided applications and declared area and second for data about provided applications and declared area grouped by plant code.

Prepared TopoJSON file which will be used in a Shape map later.

### General data

### Step 1:
Since we have tables about declarations for each year since 2020, which are freezed immediately after declaration period and I also wanted to use plant code ID instead of plant code, had to write a script to extract information from main table and apply date restrictions for each year, depending when declaration period has ended.

![Picture1](https://github.com/user-attachments/assets/4015f897-f229-45b5-9fa7-c96989117f5a)


Had to link 5 different tables to provide information about declared applications and declared area restricted to document type. And since main table doesn‘t provide information about municipalities, had to use domicile id from documents table and 2 other tables to provide municipalities names.

### Step 2: 
Extracted information for each year and saved to folder as csv files.

![Picture2](https://github.com/user-attachments/assets/cf37a460-8f43-490f-929c-d00e21fea00b)

### Step 3:

Since we use names and ID’s from “Registru centras”, took excel file from https://www.registrucentras.lt/ with information about municipalities, IDs, coordinates and etc.

### TopoJSON file preparation.

### Step 1: 
Took GeoJSON file from https://www.registrucentras.lt/. 

### Step 2: 
Imported file to https://mapshaper.org/.

### Step 3: 
After conversion to TopoJSON, power BI couldn’t read the file, so had to change EPSG code (coordinates system) from 3346 to 4326. 

![Picture3](https://github.com/user-attachments/assets/4aba18c9-eadd-47b7-9912-61929cdd8748)

Map became a bit leaned in mapshaper, however power BI read it as it suppose to be.

![Picture4](https://github.com/user-attachments/assets/e20161f9-e8a9-4db2-bb09-a5475041deb5)

Map became a bit leaned in mapshaper, however power BI read it as it suppose to be.

### Insights:

14 dashboards were. Wrote DAXs to filter relevant data, to change number format, to relate choropleth maps with legends and etc.

.pbix files and explanations are provided into branches of this repository. Not all files are provided, since steps of creating some dashboards are very similar.

### Links to all works:

1.	Change in provided applications and declared area in 2015-2024:

https://app.powerbi.com/view?r=eyJrIjoiNjdiZjUwNmEtODc1NC00NmY0LThkZDEtMDA0MDczOGI0Mzg0IiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

2.	Change in arable land and permanent pastures-grasslands declared area:

https://app.powerbi.com/view?r=eyJrIjoiZjUyNTJiYWYtMTgyZi00OTc3LTliZmQtNWI0Nzc3OGRiNDI3IiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

3.	Change in arable land declared area by municipalities (choropleth map):

https://app.powerbi.com/view?r=eyJrIjoiNWYyYWUzOGEtYmFhNy00OTQyLThkNTYtNzliMjE2N2NiNjc0IiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

4.	Change in permanent pastures-grasslands declared area by municipalities (choropleth map):

https://app.powerbi.com/view?r=eyJrIjoiN2I2NDRhOTYtZDIwNi00ZjhiLWFiZTgtZmYwMzg3ZTE3ZjZkIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

5.	Distribution of declared area of different areas and crop groups:

https://app.powerbi.com/view?r=eyJrIjoiYzVmODYyZDEtNmFiOS00ZTQ1LWI5OWQtYzNkYTIwM2EyNjAxIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

6. 	Change in crops declared area in 2023-2024 (yoy)

https://app.powerbi.com/view?r=eyJrIjoiMmI3ZjA5YjUtMGUzNi00MDc0LWEyN2YtZjAyYmY3NzU0YzkzIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

7.	Provided applications and declared area of support action "Kraštovaizdžio elementų priežiūra":

https://app.powerbi.com/view?r=eyJrIjoiYjNhMmY1ZmUtOGZiMy00ZmUwLWI0ZjMtNmRmY2M3NGRkN2ZjIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

8.	Provided applications and declared area of support action "Ekologinės sistemos":

https://app.powerbi.com/view?r=eyJrIjoiMDUxNDAxNzktMmI5Yy00MTk2LWI5ZGEtODU4ODI4YzlmMzAzIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

9.	Provided applications and declared area of support action "Veiklos ariamojoje žemėje":

https://app.powerbi.com/view?r=eyJrIjoiNWE4YWYzYjUtZDhjMy00NjkwLTlkODctNGZjODNlZTY2ZWMzIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

10.	 Provided applications and declared area of support action "KPP 2014–2020 m. ir SP 2023–2027 m.":

https://app.powerbi.com/view?r=eyJrIjoiNDc1MzE0MDMtZTRlMy00MjFkLTliMDAtYWNiZGI0ZDhlYmEwIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

11.	 Declared area of crops in 2015-2024:

https://app.powerbi.com/view?r=eyJrIjoiNDUzNGYyZDUtODFmZC00MTg4LWEzY2ItNDQ5MGFiOTljOWNlIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

12.	 Change in winter cereals declared area in 2023–2024 (choropleth map):

https://app.powerbi.com/view?r=eyJrIjoiYWQ1YjQ3ZGMtOGQxNi00MGI1LTliMzAtZjhkY2YwYTY2NzliIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

13. Change in spring cereals declared area in 2023-2024 (choropleth map):

https://app.powerbi.com/view?r=eyJrIjoiN2ViN2ZkN2ItZDg0Ni00YzE1LTkyOTktZTg1MjliMWMxYjJjIiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9

14. Change in spring and winter rapeseed declared area in 2023-2024 (choropleth map):

https://app.powerbi.com/view?r=eyJrIjoiZGE2MWY3NzctZTBlMy00NWQxLWJkZmYtYzI4Yjg4ZTI3YzM2IiwidCI6IjNjMjk2MzFmLTAyN2EtNGFlYy05OGQxLWJlMGNjODg4MzAxNiIsImMiOjl9
