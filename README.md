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