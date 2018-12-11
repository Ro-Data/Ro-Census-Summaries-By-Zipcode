# Overview

Demographic data by ZIP code can be useful in getting a better understanding of your members and/or user base. Are your members from urban or rural areas? How much money do they likely make? How educated are they? Where do they fall as far as demographics go?

The [Census Bureau American FactFinder](https://factfinder.census.gov/faces/nav/jsf/pages/community_facts.xhtml) is a free source of comprehensive and detailed data. Unfortunately, it’s not particularly easy to use in its raw format.

We’ve pulled, cleaned, consolidated, and reformatted the Census Bureau data. The enclosed tables (.txt format) should be easily uploadable into any database. These tables are:
- social.txt (Census Bureau Tables DP02 and DP02PR)
- econ.txt (Census Bureau Table DP03)
- housing.txt (Census Bureau Table DP04)
- demo.txt (Census Bureau Table DP05)
- rural_urban.txt (Census Bureau Table P2)

# What is a ZCTA5?

**None of these tables actually have a field called “ZIP code.” Rather, they have a field called “ZCTA5”.** A ZCTA5 (or ZCTA) can be thought of as interchangeable with a zip code given following caveats:
- There are no ZCTAs for PO Box ZIP codes - this means that for 42,000 US ZIP Codes there are 32,000 ZCTAs.
- ZCTAs, which stand for Zip Code Tabulation Areas, are based on zip codes but don’t necessarily follow exact zip code boundaries. If you would like to read more about ZCTAs, please refer to [this link](https://www.census.gov/geo/reference/zctas.html). The Census Bureau also provides an [animation that shows how ZCTAs are formed.](https://www.census.gov/geo/reference/zcta/zcta_delin_anim.html)

# How can I load this data into tables on AWS Redshift?
To load this data into tables on AWS Redshift, we first stored it in an Amazon S3 bucket, and then used a COPY command to load the data.
```
COPY 'AWS Redshift destination'
FROM 'S3 Bucket source'
ACCESS_KEY_ID ''
SECRET_ACCESS_KEY ''
DELIMITER '\t'
IGNOREHEADER 1;
```

# How can I load this data into Pandas?
```
import pandas as pd
pd.read_csv('filename', sep = '\t')
```

# How current is this data?

We used the 5-year estimates as opposed to the 1-year estimates because although they are less current, they are the most reliable and precise, containing data for all ZCTA's. If you would like to get a better understanding of the differences between the 1-year, 3-year, and 5-year estimates, please refer to [this link.](https://www.census.gov/programs-surveys/acs/guidance/estimates.html) For more general information on the ACS estimate files, please refer to [this handbook.](https://www.census.gov/content/dam/Census/library/publications/2018/acs/acs_general_handbook_2018_ch03.pdf)

The rural/urban summary calculation is only done once every decade, so that data is only as recent as 2010.

# General column naming rules

The Census Bureau column names aren't particularly easy to use for data analysis and don't necessarily maintain all the information for that field (such as what denominator is used for percent fields), so we reformatted them while attempting to keep the column names as detailed as possible.

```
Format:
For percent fields: category-percent-numerator-of-denominator
For estimates fields: category-unit-numerator_denominator

Examples:
Estimate; SEX AND AGE - 20 to 24 years -> sex_and_age-population-20_to_24_years_total_population
Percent; ROOMS - Total housing units - 1 room -> rooms-percent-1_room-of-total_housing_units
```
