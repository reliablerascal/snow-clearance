# Chicago's Sidewalk Snow Clearance: The North Side Complains, the South Side Gets Fined

This data analysis supports a two-part series for South Side Weekly:
<ul>
<li><strong><a href="https://southsideweekly.com/sidewalk-plowing-pilot-planned-for-next-winter/">Part I: Sidewalk-Plowing Pilot Planned for Next Winter</a></strong> explores Chicago's proposed Plow the Sidewalks Ordinance, while highlighting the disparity between a high concentration of unshoveled sidewalk complaints on the North Side vs. the high concentration of fines levied on the South Side.
<li><strong><a href="https://southsideweekly.com/chicago-snow-shovel-fines-plow-the-sidewalks-disparity">Part II: Fines Don’t Shovel Sidewalks, But Chicago Levies Them Anyway</a></strong> explores variation in snow clearance enforcement strategies by ward and across three different city department. Greater Englewood has the highest concentration of snow clearance fines, primarily issued by the Department of Streets and Sanitation. However, most fines citywide are issued by the Chicago Department of Transportation.
</ul>
 
## Key Findings
My key findings for Part I are as follows:
* <strong>3-1-1 complaints</strong> about unshoveled sidewalks are concentrated on the North Side.
   * **Lincoln Square** ranks first with an average of fifty-seven complaints per 10,000 residents each year between 2019 and 2023.
   * South and West Side communities have the fewest, with **West Pullman** last at only two complaints per 10,000 residents.
* Preliminary analysis of Department of Administrative Hearings <strong>snow clearance fines</strong> data shows eight of the ten community areas with the most hearings for fines per capita are on the South Side.
   * **Englewood**, which ranks forty-ninth in 3-1-1 complaints, had the most administrative hearings per capita since 2019, and the highest amount of fines levied.
   * **Lincoln Square**, which ranks first in 3-1-1 complaints, was twenty-second in administrative hearing dockets per capita.

To facilitate investigation of aldermanic prerogative in snow clearance efforts, I summarized data by ward rather than community area for Part II. Each ward has a roughly equal population, eliminating the need for per capita analysis. The downside is that for many readers, wards may be more difficult to identify than community area names. My key findings are as follows. 
* <strong>Roughly 3/4 of snow clearance fines are issued by the Chicago Department of Transportation (CDOT)</strong>, and about 1/4 by the Department of Streets and Sanitation (DSS).
* <strong>The rate of CDOT citations varies dramatically by ward</strong>. CDOT issues one citation per three complaints in the 23rd ward, compared to a citywide median of one per fifteen complaints. But some CDOT citations are issued proactively rather than in response to 311 calls, according to a department spokesperson.
* <strong>The rate of DSS citations also varies dramatically by ward, with the highest rates in Greater Englewood's 15th, 16th, and 6th wards</strong>. Alders provided different reasons for issuing fines, with one Greater Englewood alder saying it's part of a strategy to target vacant properties.
* <strong>Police issued only 25 citations over 4 years, but 10 of these were in Greater Englewood</strong>.

## Data sources
|Data Source|Description|
|---|---|
|[311 Service Requests](https://data.cityofchicago.org/Service-Requests/311-Service-Requests/v6vf-nfxy/about_data)|Dataset including all 311 requests for service, including uncleared sidewalks|
|[CMAP Community Data Snapshot](https://datahub.cmap.illinois.gov/datasets/CMAPGIS::community-data-snapshots-raw-data-2014-2022/explore?layer=21) |Demographic data including 2020 census population, organized by Chicago's 77 Community Areas|
|Chicago Department of Administrative Hearings- Snow Clearance Fee Citations|Response to FOIA request H064920-011124|

## Overview of Data Preparation and Analysis

Data preparation involved the following steps:
* Acquire census data, 311 complaints data, and FOIA-requested data on citations/fines for uncleared sidewalks
* Prepare data by parsing dates and snow seasons, and cleaning addresses to prepare for geocoding
* In **QGIS**:
    <ol>
    <li>gather files- points (CSV of snow clearance fines and addresses) and shapes (Chicago community areas GeoJSON)
    <li>import fines/addresses as Delimited Text Layer
    <li>geocode addresses using MMQGIS
    <li>review and correct any addresses that couldn't be geocoded, then repeat geocoding if necessary
    <li>import Chicago Community Areas regions GeoJSON
    <li>perform point-in-polygon spatial join
    <li>export geocoded data as fines-geocoded-communities.csv
    </ol>

Data aggregation and analysis is summarized in [notebooks/02-analysis/](notebooks/02-analysis/). Final results shared with editorial staff are summarized in:
* [notebooks/02-analysis/plow-01a-summarize-311-complaints.ipynb](notebooks/02-analysis/plow-01a-summarize-311-complaints.ipynb)
* [notebooks/02-analysis/plow-01b-summarize-fines-by-community.ipynb](notebooks/02-analysis/plow-01b-summarize-fines-by-community.ipynb)
* [notebooks/02-analysis/fines-02-graphics-for-ssw.ipynb](notebooks/02-analysis/fines-02-graphics-for-ssw.ipynb)

## What I Learned, Specific to Technology
After an initial period of ad-hoc data analysis, I developed a more structured data pipeline specific to multistep transformations including geocoding and spatial joins. This required significant extra effort, but made subsequent data analysis faster and more straightforward.

## Data Quirks and Other E-Varmints Standing in My Righteous Path
<ul>
<li>
Due to typos and mispellings of addresses in the Administrative Hearings data on snow clearance fines, some manual cleaning was required.
<li>I hoped to find a dataset of vacant properties that I could join to addresses identified in snow clearance fines, but according to a source at the Cook County Assessor's office such a dataset may not exist.
</ul>

## Guide to the Repository
This repository is organized as follows. Note that some data including FOIA responses and court docket respondent names were removed to protect confidentiality.

* [data](data/)- nongeographic data
   * [00-raw](data/01-raw/) source data in its original format
   * [01-tidied](data/01-tidied/) transformed, parsed, normalized data without calculated fields
   * [02-geocoded](data/02-geocoded/) dockets-to-addresses.csv geocoded by address to get lat & long coordinates
   * [03-spatially-joined](data/03-spatially-joined/) dockets-to-addresses.csv joined to Chicago ward and community areas
   * [04-standardized](data/04-standardized/) dockets-to-addresses.csv joined to Chicago ward and community areas
   * [05-finalized](data/05-finalized/) all finalized data preparation copied into this one location
* [gis](gis/)- geographic data, including QGIS work in geocoding and spatially joining data
* [notebooks](notebooks/)- data preparation and analysis in Python
   * [01-data-preparation](notebooks/01-data-preparation/) notebooks for data pipeline which normalize, geocode, and standardize data
   * [02-analysis](notebooks/02-analysis/) analysis notebooks which summarize data
* [results](results/)- analysis results for mapping & charting (e.g. in DataWrapper and Flourish)