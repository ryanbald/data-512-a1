## A1: Data Curation

The goal of this assignment is to acquire, process, and analyze a dataset of monthly traffic on [English Wikipedia](en.wikipedia.org) from December 2007 to September 2018, inclusively. The steps taken are meant to be fully reproducible.

### Wikimedia APIs

* [Legacy Pagecounts API](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts) (used to fetch monthly view counts between December 2007 and July 2016, inclusively)

* [Pageviews API](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews) (used to fetch monthly view counts between July 2015 and September 2018, inclusively)

Endpoint documentation for both APIs can be found here: https://wikimedia.org/api/rest_v1/

### Data Schema

During the data pipeline process, monthly view count data is fetched from multiple API calls and processed/consolidated into one CSV file. Here is the final schema for the data:

|**Column**             |**Value**|**Description**                                                                  |
|-----------------------|---------|---------------------------------------------------------------------------------|
|year                   |YYYY     |Year of month's view count data                                                  |
|month                  |MM       |Month of month's view count data                                                 |
|pagecount_all_views    |num_views|Month's total view count, fetched from Legacy Pagecounts API                     |
|pagecount_desktop_views|num_views|Month's desktop site view count, fetched from Legacy Pagecounts API              |
|pagecount_mobile_views |num_views|Month's mobile site view count, fetched from Legacy Pagecounts API               |
|pageview_all_views     |num_views|Month's total view count, fetched from Pageviews API                             |
|pageview_desktop_views |num_views|Month's desktop site view count by users, fetched from Pageviews API             |
|pageview_mobile_views  |num_views|Month's mobile site view count (app and web) by users, fetched from Pageviews API|

### Special Considerations

* As noted in the Wikimedia APIs section above, there is roughly a year overlap where both APIs provide monthly view count data. During this overlap, data from both APIs is stored and plotted. View counts differ between APIs during this overlap because the newer Pageviews API allows users to filter out non-user initiated page views (crawlers, spiders, bots, etc.), while the older Legacy Pagecounts API does not have this ability.
* The Pageviews API provides monthly view count data for the mobile application and the mobile web site. These values are combined to form the monthly _mobile_ site view count.
* When fetching monthly view count data with both Wikimedia APIs, the end month used as part of the API call is exclusive. The API call will fetch monthly data for all months from the start month up to, but not including, the end month.

[Wikimedia's Terms of Use](https://foundation.wikimedia.org/wiki/Terms_of_Use/)

[Wikimedia's Privacy Policy](https://foundation.wikimedia.org/wiki/Privacy_policy)

License: MIT License
