# Dog Aging Project | Environment Data User Guide

The purpose of this document is to explain to users the structure of the environmental data curated by Core D. These data are organized in long format, and individual study participants may have multiple rows, each corresponding to a unique address, calendar time, and/or entry type. Given that DAP respondents may individually change residences, and that environmental conditions are likely to change over time, we developed a procedure for updating respondent addresses and secondary datasets as they become available. The Environment Data is structured as a longitudinal project to accommodate these changes. All respondents have a non-repeating baseline row which includes their dog id and DAP pack date. Additional rows for a participant may refer to their secondary addresses, move events, updated address information, and/or updated secondary data. For detailed information on the structure of these data, please see the Geocoding Appendix, section IV, at the end of this document. The following fields will assist users with merging and working with DAP Environment data.

## Record identification and metadata variables

| Variable      | Description |
| :--- | :----------- |
| `dog_id`      | Unique dog identifier.       |
| `address_1_or_2`   | 1 = Primary address: corresponding to the location where the dog spends the majority of its time. <br><br> 2 = Secondary address: corresponding to a secondary address where their dog spends time.<sup>1</sup>       |
| `address_month`  | Month of the entry event. For baseline entries (gm_entry_type = 1), this is the month in which the respondent joined the DAP pack.        |
| `address_year`   | Year of the entry event. For baseline entries (gm_entry_type = 1), this is the calendar year in which the respondent joined the DAP pack. |

<sup>1</sup> The proportion of time that the dog spends in its primary vs. secondary residence can be found in the HLES owner contact instrument (variable name "oc_secondary_residence_time_percentage")

## Geocoding metadata variables

The purpose of the geocoding metadata variables (prefix "gm") is to provide information pertaining to the underlying geocoding process. For detailed information about the geocoding process, please see the appendix to this document. The following metadata variables are 
provided:

| Variable      | Description |
| :--- | :----------- |
| `gm_address_type`      | Contains a value if address was geocoded via esri ArcGIS Business Analyst geocoder<sup>2</sup> (`gm_geocoder` = 1). <br><br> 1 = StreetAddress: From [ArcGIS](https://developers.arcgis.com/rest/geocode/api-reference/geocoding-service-output.htm): "A street address that differs from PointAddress because the house number is interpolated from a range of numbers. Reference data contains street center lines with house number ranges, along with administrative divisions and optional postal code information, for example, 647 Haight St, San Francisco, CA, 94117". <br><br> 2 = PointAddress: From [ArcGIS](https://developers.arcgis.com/rest/geocode/api-reference/geocoding-service-output.htm): "A street address based on points that represent house and building locations. Typically, this is the most spatially accurate match level. Reference data contains address points with associated house numbers and street names, along wit h administrative divisions and optional postal code. The X / Y and geometry output values for a PointAddress match represent the street entry location for the address; this is the location used for routing operations. The DisplayX and DisplayY values represent the rooftop, or actual, location of the address. Example: 380 New York St, Redlands, CA, 92373". |
| `gm_match_type`   | Contains a value if address was geocoded via esri ArcGIS Business Analyst geocoder (`gm_geocoder` = 1) or manually matched in ArcMap `gm_geocoder` = 3. <br><br> 1 = 'A': coordinates were Automatically found at one of the two precise levels (see `gm_addr_type`) using esri Business Analyst geocoder <br><br> 2 = 'PP': coordinates were determined from a Point Placed manually on a map following a search for this address. <br><br> 3 = 'M': Business Analyst initially returned a Match or "tie" for this address, and tied coordinates were resolved based on research and review. | 
| `gm_state_fips`   | Two-digit state FIPS code corresponding to geocoded coordinates, attained via spatial join with TIGER US census tract boundary shapefiles corresponding to the relevant years' American Community Survey (accessed via [IPUMS NHGIS](https://www.nhgis.org/)<sup>3</sup>). | 
| `gm_geocoder`   | Indicates which geocoding method/level returned the coordinates for this address (See geocoding documentation appendix below for more detailed information on this process). <br><br> 1 = esri: Matched automatically via esri Business Analyst geocoder <br><br> 2 = SmartyStreets: Matched via SmartyStreets, returning Zip9 precision<sup>4</sup> <br><br> 3 = manual: Matched via manual revision <br><br> 4 = CannotLocate: Unable to locate this address, even after manual review | 
| `gm_entry_type`   | Indicates the entry event type corresponding with each row. <br><br> 1 = Baseline entry: initial gecoding attempt based on respondent address provided in the HLES owner contact survey. <br><br> 2 = Owner Profile Update: based on an updated residential address provided in the "Update My Profile" feature of the Dog Aging Project participant portal. Users can update their profile at any time. <br><br> 3 = Annual follow-up: based on new residential address information provided in the annual HLES follow-up survey. <br><br> 4 = Secondary Data Update: reflects a secondary data update entry. These entries link the most up to date address for each respondent with updated secondary data, where applicable, and always correspond with a month of 12. <br><br> 5 = Secondary Data Update + Owner Profile Update: A value of 5 reflects incidents when a respondent has provided an updated address in their owner profile portal, and this updated address is simultaneously linked to updated secondary data. <br><br> 6 = Secondary data update + Annual follow-up: Secondary data update and new annual follow-up address provided occurs in the same month-year. <br><br> 7 = Manually corrected address: reflects a manually corrected address. In these cases, a respondent provides a non-geocodable address in their initial HLES Owner Contact form. We reach out to respondents for clarification, and if they provide corrections, we geocode this corrected address. NOTE: This procedure was discontinued in October 2020. The time required to reach out to respondents was cost prohibitive when compared to compared to the limited number of corrections that were actually made. |
| `gm_complete`   | Indicates whether a given record's geocoding processing is complete. All addresses in a Curated Data Release will be marked "complete" (2) except unmatchable addresses (corresponding to gm_geocoder = 4), which will be marked "unverified" (1) for this field. <br><br> 0 = incomplete. <br><br> 1 = unverified. <br><br> 2 = complete |

<sup>2</sup> For more information about ArcGIS Business Analyst, see this link: https://www.esri.com/en-us/arcgis/products/arcgis-business-analyst/overview

<sup>3</sup> Steven Manson, Jonathan Schroeder, David Van Riper, and Steven Ruggles. IPUMS National Historical Geographic Information System: Version 14.0 [Database]. Minneapolis, MN: IPUMS. 2019. http://doi.org/10.18128/D050.V14.0

<sup>4</sup> SmartyStreets was removed from the geocoding process in late 2023.

## Contextual variables

Successfully geocoded respondent addresses are linked to pre-existing environmental indicators. The following four sections briefly describe the contextual variables linked to geocoded respondent addresses: 

1. Census Tract-level Socio-demographic and Economic Indicators

2. Census Tract-level Air Pollution Indicators

3. County-level Temperature and Precipitation Measures

4. Neighborhood Walkability Indicators

For a more detailed discussion of these environmental data, please see:

Xue D, Collins D, Kauffman M, Dunbar M, Crowder K, Schwartz SM; Dog Aging Project Consortium; Ruple A. Big data from small animals: integrating multi-level environmental data into the Dog Aging Project. Rev Sci Tech. 2023 May;42:65-74. English. doi: 10.20506/rst.42.3349. PMID: 37232318.


### 1 - Census Tract-level Socio-demographic and Economic Indicators

Socio-demographic and economic information come from the US Census<sup>5</sup>, and are provided at the census tract level. We include descriptive tract information; race/ethnicity variables; tract gender breakdown; socioeconomic status (SES) variables; and neighborhood stability variables. Each census variable provided contains the prefix "cv".

#### Descriptive Tract Information
| Variable      | Description |
| :--- | :----------- |
| `cv_population_estimate`      | Estimated tract population from ACS.       |
| `cv_area_sqmi`   | Square mileage of tract. |
| `cv_population_density` | Persons per square mile (`cv_population_estimate`/`cv_area_sqmi`). |
| `cv_data_year` | Indicates ACS release year. For example, 1 = 2018 5-year ACS; 2 = 2019 5-year ACS, etc. |

#### Race/Ethnicity Variables: All variables are converted from counts to percent based on estimated tract population (`cv_population_estimate`)

| Variable      | Description |
| :--- | :----------- |
| `cv_pct_nothispanic_white`| Percent Not Hispanic, White Alone.       |
| `cv_pct_nothispanic_black`| Percent Not Hispanic, Black Alone.       |
| `cv_pct_nothispanica_ian` | Percent Not Hispanic, American Indian and Alaska Native Alone. |
| `cv_pct_nothispanic_asian` | Percent Not Hispanic, Asian Alone. | 
| `cv_pct_nothispanicn_hpi` | Percent Not Hispanic, Native Hawaiian and Other Pacific Islander Alone. |
| `cv_pct_nothispanic_other` | Percent Not Hispanic, Some Other Race Alone. |
| `cv_pct_nothispanic_two_or_more` | Percent Not Hispanic, Two or More Races. |
| `cv_pct_hispanic` | Percent Hispanic or Latino (not broken down by race). |

#### Gender: Variable is converted from count to percent based on estimated tract population 

| Variable      | Description |
| :--- | :----------- |
| `cv_pct_female` | Percent Female. |

#### Socioeconomic/SES Variables: 

| Variable      | Description |
| :--- | :----------- |
| `cv_median_income` | Median Household Income in the Past 12 Months (In Inflation-Adjusted Dollars for current data year). |
| `cv_gini_index ` | Gini Index of Income Inequality. |
| `cv_pct_below_125povline` | Percentage of tract population below 1.25% of the poverty line. |
| `cv_pct_jobless16to64mf` | Percentage of tract population ages 16-64 unemployed in the labor force AND not in the labor force, males & females combined. | 
| `cv_pct_famsownchild_female_led` | Percentage of own children living in households with female householder, no husband present. |
| `cv_pct_less_than_ba_degree` | Percentage of population 25 years or older with less than a Bachelor's Degree. | 
| `cv_pct_less_than_100k` | Percentage of Households Earning Under $100,000 in the Past 12 Months (In Inflation-Adjusted Dollars corresponding to that data year). |
| `cv_disadvantage_index` | Disadvantage Index: Calculated by taking average z-score of 5 preceding variables. | 

#### Neighborhood Stability:
 Variable      | Description |
| :--- | :----------- |
| `cv_pct_same_house_1yrago` | Percent in Same House 1 Year Ago. |
| `cv_pct_owner_occupied` | Percent Owner Occupied Housing Units. |
| `cv_pct_us_born` | Percent Born in United States. |
| `cv_stability_index` | Stability Index: Calculated by taking average z-score of 3 preceding variables. |

<sup>5</sup> U.S. Census Bureau. (2019). 2015-2019 American Community Survey 5-year Public Use Microdata Samples. 

### Neighborhood Atlas Area Deprivation Index

The Area Deprivation Index (ADI) is based on a measure created by the Health Resources & Services Administration (HRSA) over three decades ago, and has since been refined, adapted, and validated to the Census block group neighborhood level by Amy Kind, MD, PhD and her research team at the University of Wisconsin-Madison. It allows for rankings of neighborhoods by socioeconomic disadvantage in a region of interest (e.g., at the state or national level). It includes factors for the theoretical domains of income, education, employment, and housing quality. It can be used to inform health delivery and policy, especially for the most disadvantaged neighborhood groups. For more information about the ADI, visit the [Neighborhood Atlas](https://www.neighborhoodatlas.medicine.wisc.edu/). 

The Neighborhood Atlas Deprivation Index was supported by the National Institute on Aging of the National Institutes of Health under Award Numbers RF1AG057784 and R01AG70883 (MP: Kind/Bendlin), The National Institute on Minority Health and Health Disparities of the National Institutes of Health under Award Numbers R01MD010243 (PI: Kind), The University of Wisconsin School of Medicine and Public Health (UWSMPH) Center for Health Disparities Research and The Department of Medicine.

| Variable      | Description |
| :--- | :----------- |
| `adi_nat_rank` | National percentile of block group ADI score. |
| `adi_state_rank` | State-specific decile of block group ADI score. | 
| `adi_data_year` | Indicates data source year. 1, 2015 ADI; 2, 2020 ADI; 3, 2022 ADI. |

Kind AJH, Buckingham W. Making Neighborhood Disadvantage Metrics Accessible: The Neighborhood Atlas. New England Journal of Medicine, 2018. 378: 2456-2458. DOI: 10.1056/NEJMp1802313. PMCID: PMC6051533.

University of Wisconsin School of Medicine Public Health. 2015 Area Deprivation Index v4.0.1, 2020 Area Deprivation Index v4.0.1, and 2022 Area Deprivation Index v4.0.1. Downloaded from https://www.neighborhoodatlas.medicine.wisc.edu/ July 5, 2024.

### 2 - Census Tract-level Air Pollution Indicators

Air pollutant concentration data come from public-use estimates developed by the Center for Air, Climate and Energy Solutions (CACES) using v1 empirical models as described by Kim et al. (2018)<sup>6</sup>. The most recent data are from 2015 ([available here](https://www.CACES.us/data)) and include model-based census tract level estimates for six pollutants. From CACES:

_"These models provide estimates of outdoor concentrations for six pollutants (four gases: O3, CO, SO2, NO2; two aerosols: PM10, PM2.5) throughout the contiguous U.S. Model estimates are annual-average values for years 1979 - 2015 (SO2, NO2), 1988 - 2015 (PM10), 1990-2015 (CO), 1999-2015 (PM2.5), and the average during May through September of the daily maximum 8-hour moving average for years 1979-2015 (O3). When downloading data, concentrations are listed as the variable "pred_weight"; units are micrograms per cubic meter for PM2.5 and PM10, parts per billion for ozone, SO2, and NO2, and parts per million for carbon monoxide. Data are available at national, state, county, census tract, and census block group levels."_ 

These data are merged to geocoded respondent addresses using their 11-digit tract FIPS code. 

| Variable      | Description |
| :--- | :----------- |
| `pv_co` | Carbon monoxide (ppm). |
| `pv_no2` | Nitrogen dioxide (ppb). |
| `pv_o3` | Ozone (ppb). |
| `pv_pm10` | Particulate matter ($\mu$g/m3). |
| `pv_pm25` | Particulate matter ($\mu$g/m3). |
| `pv_so2` | Sulfur dioxide (ppb). |
| `pv_complete` | Indicates whether a given record's pollutant data variables are complete. All geocoded addresses should be marked "complete" (2) except AK & HI addresses<sup>7</sup>, which will be marked "unverified" (1) for this field. <br><br> 0 = Incomplete <br><br> 1 = Unverified <br><br> 2 = Complete. |
| `pv_data_year` | Indicates the year of associated pollutant data. Currently only one option exists. <br><br> 1 = 2015 CACES |

<sup>6</sup> Kim, S. Y., M. Bechle, S. Hankey, L. Sheppard, A. A. Szpiro, and J. D. Marshall. 2018. "A Parsimonious Approach for Estimating Individual-Level Concentrations of Criteria Pollutants over the Contiguous US." Environ Health Perspect. 
<sup>7</sup> NOTE: Pollutant levels are estimated ONLY for the contiguous US, excluding Alaska & Hawaii. Respondents with addresses in AK and HI will have their pollutant instrument missing and marked "unverified" in this variable. . 
The field "pv_complete" will be given a "1", corresponding to "unverified", and all other geocoded addresses will have a "2" (corresponding to "complete") for this field. Addresses that are unable to be geocoded (gm_geocoder = 4) will have a "0" for this field.

### 3 - County-level Temperature and Precipitation Measures

Temperature and Precipitation variables data come from NOAA's Climate Divisional Database ([nClimDiv](ftp://ftp.ncdc.noaa.gov/pub/data/cirs/climdiv/))<sup>8</sup>. These data are provided at the county level. NOAA provides county-level climate indicators at two temporal levels. First, annual summaries contain temperature and precipitation averages for each month of each year. Second, "normal summaries" are provided, which are long-term averages over 30-year periods in increments of 10 years. Both annual and normal variables are linked to respondent addresses. 

#### Annual Summaries  

We include monthly summaries for the most recent year available.

| Variable      | Description |
| :--- | :----------- |
| `tp_data_year` | Indicates the year that monthly values correspond with based on the calendar year in which the responded lived at a primary or secondary address. 1 = nClimDiv 2019; 2 = nClimDiv 2020, etc. |
| `tp_tmin_annual_XX` | Monthly minimum temperature, where "XX" is equal to a two-digit number corresponding to month (ie, 01 = January; 02 = February, etc.). |
| `tp_tmax_annual_XX` | Monthly maximum temperature. |
| `tp_tmpc_annual_XX` | Monthly average temperature. |
| `tp_pcpn_annual_XX` | Precipitation (inches) . |

#### Normal Summaries

Monthly long-term averages in 30 year periods in increments of 10 years. 

| Variable      | Description |
| :--- | :----------- |
| `tp_norm_data_year` | Indicates the 30-year period that monthly values correspond with. 1, nClimDiv 1981-2010; 2 = 1991-2020, etc. |
| `tp_tmin_norm_XX` | Monthly minimum temperature, where "XX" is equal to a two-digit number corresponding to that month (ie, 11 = November; 12 = December, etc.). |
| `tp_tmax_norm_XX` | Monthly maximum temperature. | 
| `tp_tmpc_norm_XX` | Monthly mean temperature. |
| `tp_pcpn_norm_XX` | Precipitation (inches). |

This yields a total of 48 annual summary monthly variables (12 months * 4 variables[tmin, tmax, tmpc, and pcpn]) as well as 48 long-term normal summary monthly variables, resulting in 96 total substantive contextual climate variables linked to each residential primary and secondary addresses. 

NOTE: Not all US regions are included in the NOAA nClimDiv. For such instances, we undergo the following procedures: 
- Hawaii and Washington DC: NOAA nClimDiv county-level summaries do not include Hawaii counties or Washington, DC. For these regions, we constructed our own climate variables by downloading the individual station-level data from NOAA in each jurisdiction, geocoding them, and averaging out the monthly readings by county. This procedure is repeated for both annual and normals periods. 
- Ad Hoc missing regions in contiguous US: Some contiguous counties are missing from the NOAA nClimDiv, particularly small counties that are enveloped entirely within larger counties. In these instances, we provide 
the climate variables for the larger surrounding counties in which these smaller counties are located. To date, only one such missing county has been identified (Lexington City County, FIPS ID 51678).

<sup>8</sup> Vose, Russell S.; Applequist, Scott; Squires, Mike; Durre, Imke; Menne, Matthew J.; Williams, Claude N., Jr.; Fenimore, Chris; Gleason, Karin; Arndt, Derek (2014): NOAA's Gridded Climate Divisional Dataset (CLIMDIV). NOAA National Climatic Data Center. doi:10.7289/V5M32STR

### 4 - Neighborhood Walkability Indicators

The Walkability variables (prefix = `"wv"`) draw from two separate data sources. First, three variables are provided by Walkscore, a private company that generates a walkability index based on walking routes to nearby amenities and other indicators (see [here](https://www.walkscore.com/methodology.shtml) for more information). We use the walkscoreAPI R [package](https://cran.r-project.org/web/packages/walkscoreAPI/walkscoreAPI.pdf) to retrieve Walkscores for each geocoded address based on their geocoded lat/lon coordinates. Second, we include residential density variables from the ACS. We include these in our walkability instrument based on the conclusions drawn by Mooney et al. (2020)<sup>9</sup>, who find that residential density is an appropriate proxy measure for walkability. Residential density is calculated at the census tract level. 

#### Walkscore Variables:

| Variable      | Description |
| :--- | :----------- |
| `wv_walkscore` | A numeric score from 0-100 indicating walkability. |
| `wv_walkscore_descrip` | Walkscore's categories for walkability, based on retrieved Walkscore. <br><br> 1 = Walker's Paradise (WalkScores 90-100) <br><br> 2 = Very Walkable (WalkScores 70-89) <br><br> 3 = Somewhat Walkable (WalkScores 50-69) <br><br> 4 = Car-Dependent (WalkScores under 50) <br><br> 5 = NA (No WalkScore available for these coordinates) |
| `wv_walkscore_date` | A date indicating the last time WalkScore updated the calculated score for the data they provide. | 

#### Residential Density Variables:

| Variable      | Description |
| :--- | :----------- |
| `wv_housing_units` | Number of housing units in the tract, from American Community Survey. |
| `wv_res_density` | Housing units per square mile (`wv_housing_units`/`cv_areasqmi`). | 
| `wv_density_data_year` | Indicates data source year. 1, 2018 5-year ACS; 2, 2019 5-year ACS, etc. |

<sup>9</sup>Stephen J. Mooney, Philip M. Hurvitz, Anne Vernez Moudon, Chuan Zhou, Ronit Dalmat, Brian E. Saelens. "Residential neighborhood features associated with objectively measured walking near home: Revisiting walkability using the Automatic Context Measurement Tool (ACMT)." Health & Place, Volume 63. doi: https://doi.org/10.1016/j.healthplace.2020.102332

### Geocoding Appendix

The following appendix describes the DAP Core D geocoding process in detail for user reference. 

#### I. Adjudicating Geocoders:

Our first step in the geocoding process was to identify a geocoder which could match respondent addresses with the greatest degree of accuracy. We tested the first several hundred submitted respondent addresses against three popular geocoders: 1) esri's Business Analyst 2019 data, which is similar to their ArcGIS StreetMap Premium project; 2) SmartyStreets, an online API based geocoder; and 3) the "geocode" function in the R package ggplot2, which uses the Google geocoding API. 

The first 542 addresses were geocoded against all three services. The esri Business Analyst geocoder returned the most complete results and was capable of matching 97.8% of the addresses at a high quality (rooftop or street address) level. SmartyStreets was able to match 95.4% of the addresses at a high-quality level (Zip9 or higher), and the Google API was able to match 96.5% of the results at some level (accuracy score not available). 

A manual review and coordinate distance analysis led us to approach the geocoding procedure in a series of three "levels". The following procedure will be run for primary and (when applicable) secondary residencies where the dog spends time (as indicated in owner contact survey):

| Level      | Description |
| :--- | :----------- |
| Level 1: esri | Addresses will be run through the esri Business Analyst geocoder; the "gold standard" based on our pilot analysis. Precisely matched addresses are taken at face value and take on the following values: <br><br> `gm_match_type` = 'A' if not tied in address locator; 'M' if tied and manual match performed. <br><br> `addr_type` = 'PointAddress' or 'StreetAddress' (the two acceptable "precise" matching scores). <br><br> `gm_geocoder` = 'esri'. <br><br> The ~3% of addresses that cannot be matched at the rooftop or street address level will then proceed to level 2. | 
| Level 2: SmartyStreets | Poorly matched addresses (matched at the street name or zip code level in esri) will then be run through the SmartyStreets geocoder. SmartyStreets is preferred because it provides users with an accuracy score. If addresses which have proceeded to level 2 can be geocoded at SmartyStreets' highest accuracy level (Zip9, typically block-level), then these coordinates are taken at face value and take on the following values: <br><br> `gm_match_type` = 'NA'. <br><br> `addr_type` = 'NA'. <br><br> `gm_geocoder` = 'SmartyStreets'. <br><br> All others proceed to level 3. | 
| Level 3: Google maps & manual review |  Our pilot analysis indicated that approximately 1% of addresses proceeded to level 3, and were not able to be precisely matched by either esri or SmartyStreets geocoder. In these instances, we will proceed with a manual review using Google Maps and human research. Addresses matched at level 3 will take the following values: <br><br> `gm_match_type` = 'PP'. <br><br> `gm_address_type` = 'NA'.<br><br> `gm_geocoder` = "manual". |
| Unmatchable Addresses | In some cases addresses still cannot be matched (perhaps due to respondent entry errors, rural addresses, or new build development). Prior to October 2020, Core D reached out to the respondent in an effort to clarify their location. If respondents provided an updated address, the geocoding process was re-run for this newly provided address. Such addresses will reflect `gm_entry_type` = "7" ("Manually corrected address").<br><br>Core D stopped reaching out to respondents to manually correct addresses in October 2020 due to the overwhelming costs. Resulting unmatchable addresses (both primary and secondary) will take the following values: <br><br> `gm_geocoder` = 'CannotLocate'. <br><br> `gm_complete` = "Unverified".|

See metadata documentation above for detailed information on the geocoding metadata variables (prefix = "gm") included. 

#### II. Spatially joining coordinates to census boundaries 

Precisely-matched coordinates are then plotted over the TIGER US census tract boundary shapefiles corresponding to the relevant years' American Community Survey (accessed via IPUMS NHGIS<sup>10</sup>). Using the spatial join tool in ArcMap, the block group information that each respondent address point falls within is joined to the respondents' study id. 

#### III. Merging to secondary datasets

##### Census Variables (prefix = "cv")
Once each address is assigned a block-group level FIPS code, chosen relevant neighborhood characteristics are merged with each respondents' record using the 11-digit tract FIPS code as the join key. This creates a matrix of respondent study ID, tract FIPS code, and relevant census variables. For a complete list of census variables selected, see Census Variable documentation above. 

##### Neighborhood Atlas Area Deprivation Index Variables (prefix = "adi")
Once each address is assigned a block-group level FIPS code, ADI metrics are merged with each respondents' record using the 11-digit tract FIPS code as the join key. This creates a matrix of respondent study ID, tract FIPS code, and relevant ADI variables. For a complete list of ADI variables selected, see Neighborhood Atlas Area Deprivation Index Variable documentation above. 

##### Pollutant Variables (prefix = "pv")
 Pollutant concentration data come from public-use estimates developed by the Center for Air, Climate and Energy Solutions (CACES) using v1 empirical models as described by Kim et al. (2018)<sup>11</sup>. These data are merged to geocoded respondent addresses using their 11-digit tract FIPS code.
 
##### Temperature and Precipitation Variables (prefix = "tp")
Temperature and precipitation variables come from the NOAA's Climate Divisional Database (nClimDiv), which makes available four key climate indicators (maximum air temperature, minimum air temperature, average air temperature, and precipitation in inches) for nearly every census county in the contiguous US and Alaska, both annually (dating back to 1895) and in long-term 30-year averages in increments of 10 years ("normals"). We include these four monthly variables for the most recent calendar year as well as the four monthly variables for the most recent "normals" period. This results in 96 total climate variables included (12 months * 4 variables * 2 periods). For in-depth description of these variables, see climate variables documentation above. 

##### Walkability Variables (prefix = "wv")
Walkability variables come from two sources: Walkscore and ACS. Walkscore variables include the proprietary "Walkscore" (an integer between 0-100), as well as the corresponding walkability category according to Walkscore. The ACS walkability indicator included is residential density (estimated number housing units in each tract divided by tract square mile). See neighborhood walkability documentation above for more details. 

#### IV. Residential and Extra-local changes

New DAP pack members' residential addresses will be geocoded on a regular basis. Baseline entries will have the "gm_entry_type" = 1 in their gm_entry_type field, corresponding with baseline entry. Residential and extra-local changes are then treated as follows: 

##### Individual Moves
"Ad-Hoc" revision: On a regular basis, DAP participant user profile updates reflecting a change in primary or secondary residences will be identified. Changed addresses will be geocoded, linked to secondary data, and imported as they occur. The address_month and address_year fields will correspond with the month and year that the user updated their profiles. Ad hoc updates will have the "Entry Type" field = "Owner profile update" in their gm_entry_type field.

##### Annual revision
In addition, all respondents will be asked to confirm their information once a year via annual check-in surveys. After these annual check-ins have been completed, we will update any newly changed addresses, geocode them, and link to corresponding environmental indicators. Annual updates will have the "Entry Type" = "Annual Follow-Up" in their gm_entry_type field. 

##### Annual data updates
Early each year, all geocoded addresses will be updated with newly available secondary data. New data will be linked to the most up-to-date respondent address and imported into the December month-year event for the preceding year (ie, December 202cd 0 for the 2021 annual update). Source data year will be indicated in the "data year" fields corresponding to each secondary data category. Data updates will have the "Entry Type" field = "Secondary data update" in their gm_entry_type field. If the data update occurs in the same month-year that an owner profile update OR an annual revision occurs, these will be indicated by "Entry Type" = "Secondary data update + Owner profile update" or "Entry Type" = "Secondary data update + Annual Follow-Up" respectively in their gm_entry_type field.

<sup>10</sup> Steven Manson, Jonathan Schroeder, David Van Riper, and Steven Ruggles. IPUMS National Historical Geographic Information System: Version 14.0 [Database]. Minneapolis, MN: IPUMS. 2019. http://doi.org/10.18128/D050.V14.0

<sup>11</sup> Kim, S. Y., M. Bechle, S. Hankey, L. Sheppard, A. A. Szpiro, and J. D. Marshall. 2018. "A Parsimonious Approach for Estimating Individual-Level Concentrations of Criteria Pollutants over the Contiguous US." Environ Health Perspect. 

*** 

###### *last updated 2025-01-14*
