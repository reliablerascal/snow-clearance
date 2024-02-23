# Chicago's Sidewalk Snow Clearance: The North Side Complains, the South Side Gets Fined

This data analysis supports a two-part series for South Side Weekly:
<ul>
<li><strong><a href="https://southsideweekly.com/sidewalk-plowing-pilot-planned-for-next-winter/">Part I: Sidewalk-Plowing Pilot Planned for Next Winter</a></strong> explores Chicago's proposed Plow the Sidewalks Ordinance, while highlighting the disparity between a high concentration of unshoveled sidewalk complaints on the North Side vs. the high concentration of fines levied on the South Side.
<li><strong>Part II: Fines Don’t Shovel Sidewalks, but the South Side Pays Anyway</strong> will explore different snow clearance enforcement strategies by three different city departments, and what types of property owners are getting fined on the South Side. 
</ul>
 
The data analysis for Part I is summarized in <a href="https://github.com/reliablerascal/snow-clearance/blob/main/notebooks/02-summarize-311-snow-complaints-by-community.ipynb">/notebooks
/02-summarize-311-snow-complaints-by-community.ipynb</a>.

## Key Findings
My key findings for Part I are as follows:
* <strong>3-1-1 complaints</strong> about unshoveled sidewalks are concentrated on the North Side. Lincoln Square ranks first with an average of fifty-seven complaints per 10,000 residents each year between 2019 and 2023. South and West Side communities have the fewest, with West Pullman last at only two complaints per 10,000 residents.
* Preliminary analysis of Department of Administrative Hearings <strong>snow clearance fines</strong> data shows eight of the ten community areas with the most hearings for fines per capita are on the South Side. Englewood, which ranks forty-ninth in 3-1-1 complaints, had the most administrative hearings per capita since 2019, and the highest amount of fines levied. Lincoln Square, which ranks first in 3-1-1 complaints, was twenty-second in administrative hearing dockets per capita.

## Data sources
|Data Source|Description|
|---|---|
|[311 Service Requests](https://data.cityofchicago.org/Service-Requests/311-Service-Requests/v6vf-nfxy/about_data)|Dataset including all 311 requests for service, including uncleared sidewalks|
|[CMAP Community Data Snapshot](https://datahub.cmap.illinois.gov/datasets/CMAPGIS::community-data-snapshots-raw-data-2014-2022/explore?layer=21) |Demographic data including 2020 census population, organized by Chicago's 77 Community Areas|
|[Chicago Department of Administrative Hearings- Snow Clearance Fee Citations](https://docs.google.com/spreadsheets/d/1TKkQvOkpihZGkiIZ_Hx-TVzoV6kXvZUETSD8h5YhlR0/edit?usp=drive_link)|Response to FOIA request H064920-011124|

## Overview of Data Analysis Process

## What I Learned
I learned to geocode and spatially join Administrative Hearings data in order to identify the community area associated with each fine.

## Data Quirks and Other E-Varmints Standing in My Righteous Path
<ul>
<li>
Due to typos and mispellings of addresses, Administrative Hearings data on snow clearance fines required extensive manual cleaning.
<li>I hoped to find a dataset of vacant properties that I could join to addresses identified in snow clearance fines, but that data is inconsistently tracked.
</ul>

## Guide to the Repository
This repository is organized as follows:

* [data](data/)- includes only my own manually-entered lookup table for CTA stations<br>
* [layers](layers/)- QGIS work in geocoding and spatially joining data
* [notebooks](notebooks/)- steps through the analysis<br>
   * [02-summarize-311-snow-complaints-by-community.ipynb](notebooks/02-summarize-311-snow-complaints-by-community.ipynb) - analysis of 311 complaints data per capita, in support of Part I<br>
* [results](results/)- results output from Jupyter Notebook for mapping & charting in DataWrapper and Flourish