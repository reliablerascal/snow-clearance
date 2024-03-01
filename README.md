# Chicago's Sidewalk Snow Clearance: The North Side Complains, the South Side Gets Fined

This data analysis supports a two-part series for South Side Weekly:
<ul>
<li><strong><a href="https://southsideweekly.com/sidewalk-plowing-pilot-planned-for-next-winter/">Part I: Sidewalk-Plowing Pilot Planned for Next Winter</a></strong> explores Chicago's proposed Plow the Sidewalks Ordinance, while highlighting the disparity between a high concentration of unshoveled sidewalk complaints on the North Side vs. the high concentration of fines levied on the South Side.
<li><strong>Part II: Fines Don’t Shovel Sidewalks, but the South Side Pays Anyway</strong> will explore different snow clearance enforcement strategies by three different city departments, and what types of property owners are getting fined on the South Side. 
</ul>
 
## Key Findings
My key findings for Part I are as follows:
* <strong>3-1-1 complaints</strong> about unshoveled sidewalks are concentrated on the North Side.
   * **Lincoln Square** ranks first with an average of fifty-seven complaints per 10,000 residents each year between 2019 and 2023.
   * South and West Side communities have the fewest, with **West Pullman** last at only two complaints per 10,000 residents.
* Preliminary analysis of Department of Administrative Hearings <strong>snow clearance fines</strong> data shows eight of the ten community areas with the most hearings for fines per capita are on the South Side.
   * **Englewood**, which ranks forty-ninth in 3-1-1 complaints, had the most administrative hearings per capita since 2019, and the highest amount of fines levied.
   * **Lincoln Square**, which ranks first in 3-1-1 complaints, was twenty-second in administrative hearing dockets per capita.

## Data sources
|Data Source|Description|
|---|---|
|[311 Service Requests](https://data.cityofchicago.org/Service-Requests/311-Service-Requests/v6vf-nfxy/about_data)|Dataset including all 311 requests for service, including uncleared sidewalks|
|[CMAP Community Data Snapshot](https://datahub.cmap.illinois.gov/datasets/CMAPGIS::community-data-snapshots-raw-data-2014-2022/explore?layer=21) |Demographic data including 2020 census population, organized by Chicago's 77 Community Areas|
|[Chicago Department of Administrative Hearings- Snow Clearance Fee Citations](https://docs.google.com/spreadsheets/d/1TKkQvOkpihZGkiIZ_Hx-TVzoV6kXvZUETSD8h5YhlR0/edit?usp=drive_link)|Response to FOIA request H064920-011124|

## Overview of Data Analysis

### Part I- 311 Complaints
1) [00-assess-data-311-snow-related.ipynb](notebooks/00-assess-data-311-snow-related.ipynb)- Review 311 complaints data structures and explore data 
2) [01-prep-snow-violations-data.ipynb](notebooks/01-prep-snow-violations-data.ipynb)- Acquire census data and 311 complaints data, parse dates and snow seasons
3) [02-summarize-311-snow-complaints-by-community.ipynb](notebooks/02-summarize-311-snow-complaints-by-community.ipynb)- Summarize 311 complaints data to identify communities with highest and lowest per capita rates of 311 complaints

### Part I- Preliminary Analysis of Fines
1) [fines-01-prep-data.ipynb](notebooks/fines-01-prep-data.ipynb)- Read snow clearance fines data, parse dates, clean addresses and prepare for geocoding
2) In **QGIS**:
    <ol>
    <li>gather files- points (CSV of snow clearance fines and addresses) and shapes (Chicago community areas GeoJSON)
    <li>import fines/addresses as Delimited Text Layer
    <li>geocode addresses using MMQGIS
    <li>import Chicago Community Areas regions GeoJSON
    <li>perform point-in-polygon spatial join
    <li>export geocoded data as fines-geocoded-communities.csv
    </ol>
3) [fines-02-summarize_ssw_part1.ipynb](notebooks/fines-02-summarize_ssw_part1.ipynb)- Summarize 311 complaints data to identify communities with highest and lowest per capita rates of 311 complaints


## What I Learned
I learned to geocode Administrative Hearings address data to get lat and long coordinates, and then spatially join this data to identify the community areas associated with each fine.

## Data Quirks and Other E-Varmints Standing in My Righteous Path
<ul>
<li>
Due to typos and mispellings of addresses in the Administrative Hearings data on snow clearance fines, some manual cleaning was required.
<li>I hoped to find a dataset of vacant properties that I could join to addresses identified in snow clearance fines, but according to a source at the Cook County Assessor's office such a dataset may not exist.
</ul>

## Guide to the Repository
This repository is organized as follows:

* [data](data/)- nongeographic data
   * [01-raw](data/01-raw/) source data in its original format
   * [02-tidied](data/02-prepped/) transformed, parsed, normalized data
   * [03-geocoded](data/03-geocoded/) dockets-to-addresses.csv geocoded by address to get lat & long coordinates
   * [03-geocoded](data/04-spatially-joined/) dockets-to-addresses.csv joined to Chicago ward and community areas
* [gis](gis/)- geographic data, including QGIS work in geocoding and spatially joining data
* [notebooks](notebooks/)- data preparation and analysis in Python
   * **fines*** prefix designates notebooks specific to analysis of fines data for Part II of the story
   * **x*** prefix designates exploratory analyses
* [results](results/)- analysis results for mapping & charting (e.g. in DataWrapper and Flourish)