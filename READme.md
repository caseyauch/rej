# Regional Environmental Justice “Plus” Communities
This repository contains data and methodology to support a project that evaluates environmental justice populations most impacted by transportation changes across the 13 Metropolitan Planning Organizations (MPO) regions. 
## About the Project
A Regional Environmental Justice “Plus” (REJ+) Community is an environmental justice population that is most impacted by transportation changes. The unit of analysis is census block groups (ACS 2020). 
To qualify as an REJ+ community, a block group must meet two thresholds:

At least one of three EJ criteria must be true:
- Annual median household income ≤ MPO 25th percentile
- Percent of Minorities ≥ MPO 75th percentile 
- Percent of Households with Limited English Proficiency ≥ MPO 75th percentile 

At least one of the following three transportation criteria must be true: 
- Percent of Households with Zero Vehicles ≥ MPO 75th percentile 
- Percent of Households with Disabilities ≥ MPO 75th percentile 
- Percent of Seniors (65+ years) ≥ MPO 75th percentile

## Prepare data
For this analysis, we expanded the statewide environmental justice (EJ) community criteria by adding three additional factors. The six factors used are household income, minority race status, limited English proficiency, car ownership, disability status, and age.  All data (saved in the Data subfolder) is available in the American Community Survey.

**Download ACS Tables**
- B03002 – Hispanic or Latino by Race
- B19013 – Median Income
- B99161 – Language Status 
- B25044 – Tenure by Vehicles Available 
- B01001 – Age
- B22010 – Receipt of Food Stamps/SNAP by Disability Status

**Minority Status:** For each block group, add the number of people who identify as Hispanic or Latino (B03002_012E) and the number of people who are non-Hispanic and non-white (B03002_002E-B03002_003E). Divide this total by the block group population to calculate the percent of people with minority status.

**Households with Limited English Proficiency (LEP):** For each block group, divide the number of allocated persons by the block group population to calculate the percent of people with LEP.

**Households with Zero-Vehicles:** For each block group, add the number of owner-occupied (B25044_003E) and renter-occupied (B25044_010E) households without access to a vehicle.  Divide this total by the block group population to calculate the percent of zero-vehicle households.

**Senior Status:** For each block group, add the number of males and females aged 65 and over and divide this total by the block group population to calculate the percent of seniors.

## Calculate Thresholds
We developed unique thresholds for each MPO region to capture regional differences in demographics across the Commonwealth.
1.	Attribute all block groups to an MPO region using the ArcGIS Intersect tool
2.	Export table with block group ID, demographic information, and MPO label (CBG_MPO_demographics_0920.xls)
3.	Filter by MPO region
4.	Calculate thresholds using numeric percentages (e.g., 25th percentile for median income) for all six indicators 
5.	Repeat steps 3 and 4 for 13 MPO regions; this was automated using Excel’s Quartile command:
```=QUARTILE(FILTER('MA Demographics 0920'!G:G, 'MA Demographics 0920'!$E:E=$A2), 1)```

| MPO Region  | Median Income | Minority Status | LEP | Disability Status | Zero-Vehicle Households | Seniors
| :------------- | :------------- | :------------- | :------------- | :------------- | :------------- | :------------- |
Berkshire	| $49,835 |	17% |	0% | 36% | 10% | 31%
Boston Region	| $72,237 |	47%	| 7%| 28% |	17% |	21%
Cape Cod	| $62,444 |	15% |	1% |	30%	| 6% | 42%
Central Massachusetts	| $53,780 |	41%	| 7% |	33%	|13%|21%
Franklin	| $51,655 |	14% |	1% |	38% |	9% |	27%
Martha's Vineyard	| $61,957 | 22% |	0% |	22% |	5%	| 35%
Merrimack Valley | $58,737 |	67% |	8%	| 32% |	10%	| 21%
Montachusett	| $53,686 | 31% |	2% |	32%	| 8%| 21%
Nantucket	| $80,312 |26%	| 1%| 32%	| 9% |	33%
Northern Middlesex	| $70,603 | 46%	| 5% |	31%	| 8% |	19%
Old Colony	| $70,178 | 51% |	4%	| 31%	| 6% |	22%
Pioneer Valley	| $43,895 |	59%	| 7%	| 37%	| 17%	| 24%
Southeastern Massachusetts |	 $49,891 |	28%	 | 8%	| 36%	| 13%	| 23%

## Create Symbology
We wrote several symbology expressions in ERSI’s Arcade scripting language to visualize which block groups meet the REJ+ criteria (saved in Symbology). 

## Build Dashboard 
To visualize the results, we developed an ESRI dashboard, hosted [here](https://massdot.maps.arcgis.com/apps/dashboards/4dec59ffffff4bd7ae119047808a1e93).

## Data Dictionary 
| Attribute Name  | Description | Data Source | Year | 
| :------------- | :------------- | :------------- | :------------- | 
Blockid | Census Block Group ID | American Community Survey | 2020
MPO | MPO Region Name | geoDOT | 2020
Median Income | Median household income | American Community Survey | 2020
Minority Status | Percent of individuals who are Hispanic or non-White | American Community Survey 
LEP | Percent of individuals with a disability | American Community Survey | 2020
Disability Status | Percent of individuals with a disability | American Community Survey | 2020 
Zero-Vehicle Households | Percent of households without a personal vehicle | American Community Survey | 2020
Seniors | Percent of individuals aged 65+ years | American Community Survey | 2020 


