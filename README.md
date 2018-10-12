# Overview

Demographic data by ZIP code can be useful in getting a better understanding of your members, but most data sources we found were either sparse in content, or costly to acquire. The most complete free-to-use data sources that we could find were the American Community Survey (ACS) 5-year estimates from the United States Census Bureau, which contain social, economic, housing, and other demographic information. We also used the P2 2010 Census Summary Table to get information on how rural/urban a particular ZCTA was. Unfortunately, the rural/urban summary calculation is only done once every decade, so the data is only as recent as 2010.

The Census Bureau does not have information by Zip Codes, so the next best alternative was to tabulate this information by Zip Code Tabulation Areas (ZCTAs). ZCTAs are generalized areal representations of United States Postal Service (USPS) ZIP Code service areas. There are approximately 42,000 ZIP Codes and 32,000 ZCTAs. The reason that there is not one ZCTA for every ZIP Code is that PO Boxes are excluded in ZCTAs, since only populated areas are included in the Census data. If you would like to read more about ZCTAs, please refer to [this link.](https://www.census.gov/geo/reference/zctas.html) The Census Bureau also provides an [animation that shows how ZCTAs are formed.](https://www.census.gov/geo/reference/zcta/zcta_delin_anim.html)

We used the 5-year estimates as opposed to the 1-year estimates because although they are less current, they are the most reliable and precise, containing data for all ZCTA's. If you would like to get a better understanding of the differences between the 1-year, 3-year, and 5-year estimates, please refer to [this link.](https://www.census.gov/programs-surveys/acs/guidance/estimates.html) For more general information on the ACS estimate files, please refer to [this handbook.](https://www.census.gov/content/dam/Census/library/publications/2018/acs/acs_general_handbook_2018_ch03.pdf)

# Data Cleaning and Formatting

The tables that we used are the P2, DP02, DP02PR, DP03, DP04, and DP05 by ZCTA from the Census Bureau, which can be accessed by using the below search selections in their [American FactFinder tool.](https://factfinder.census.gov/faces/nav/jsf/pages/searchresults.xhtml?refresh=t) There are two social characteristics tables because some columns are different for US and PR ZCTAs, which will be discussed further later.

![Rural Urban](/rural_urban.png)

This table only has 2 data fields that were used, the population in rural areas and population in urban areas by ZCTA5. Percentages for both data fields were also calculated.

![Search Selections](/search_selections.png)

For all data fields in the ACS tables, there is an entry for both _percent_ and _estimate_ as seen in the screenshot below.

![Percents and Estimates](/table_example.png)

When downloading the files from the United States Census Bureau, both of these fields are initially included. When they aren't applicable (e.g. _percent_ in the **Population 16 years and over** column, and _estimate_ in the **Unemployment Rate** columns), we dropped them from the table.  It should noted that when these tables are downloaded, each row corresponds to one ZCTA, and the columns are the different data fields.

In addition, the column names aren't particularly easy to use for data analysis and don't necessarily maintain all the information for that field (such as what denominator is used for percent fields), so we reformatted them while attempting to keep the column names as detailed as possible.

```
Format:
For percent fields: category-percent-numerator-of-denominator
For estimates fields: category-unit-numerator_denominator

Examples:
Estimate; SEX AND AGE - 20 to 24 years -> sex_and_age-population-20_to_24_years_total_population
Percent; ROOMS - Total housing units - 1 room -> rooms-percent-1_room-of-total_housing_units
```

There were some columns in the social characteristics tables (DP02 and DP02R) that did not match, and have been renamed or dropped (if a common name for the columns could not be found). The affected columns are mostly around the _year of entry_ and _residence 1 year ago_ data fields.

The five separate tables are available for download [here](https://github.com).



--------------------------------------------------------------
