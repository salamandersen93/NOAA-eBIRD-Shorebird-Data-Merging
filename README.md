# NOAA CO-OPS and eBird Data Merging -- New Jersey Shorebirds 2020-2021
Merging of NOAA CO-OPS tidal data with eBird data for shorebirds in selected coastal New Jersey counties

This is a living dataset constructed of tidal data from the National Oceanic and Atmospheric Admistration Center for Operational Oceanic Products and Services (NOAA CO-OPS) and avian observation data compiled from the citizen-science project eBird. The scope of this data is coastal New Jersey with a date range of January 2020 onward. The goal of this project is to provide a reliable data source for citizen scientists and birdwatchers to understand the relationship of shorebird sightings and tide.

Tidal information is made avaible via the NOAA CO-OPS API (documented here: https://api.tidesandcurrents.noaa.gov/api/prod/). The high_low parameter is used during request to gain access to high and low tide times and water levels. The counties with tidal data stations available are:

1. Atlantic
2. Cumberland
3. Monmouth
4. Cape May

The eBird API (documented here: https://documenter.getpostman.com/view/664302/S1ENwy59) allows users to download data of recent bird observations of birds seen in a given country, state, county, or location. Shorebirds are the focus of this project -- 23 species (listed below) were included in the eBird data request. Species selected are common to semi-common visitors to New Jersey beaches throughout various seasons. The get_observations request was used to gather data including: time of observation, species observed, quantity observed, location name, latitude, and longitude. eBird data is only available to request for the past 30 days. Due to this limitation, an additional request for data was made on the eBird website for all of New Jersey from January 2020 to present. The text file was received via email and pre-filtered using Excel PowerQuery for the relevant species then fed into a pandas dataframe within this project. The species (along with respective eBird species codes) within the context of this project are:

1. American Oystercatcher (ameoys)
2. Black-bellied Plover (bkbplo)
3. American Golden-Plover (amgplo)
4. Semipalmated Plover (semplo)
5. Piping Plover (pipplo)
6. Killdeer (killde)
7. Upland Sandpiper (uplsan)
8. Hudsonian Godwit (hudgod)
9. Marbled Godwit (margod)
10. Stilt Sandpiper (stisan)
11. Sanderling (sander)
12. Dunlin (dunlin)
13. Purple Sandpiper (pursan)
14. Least Sandpiper (leasan)
15. Pectoral Sandpiper (pecsan)
16. Western Sandpiper (wessan)
17. Short-billed Dowitcher (shbdow)
18. Long-billed Dowitcher (lobdow)
19. Spotted Sandpiper (sposan)
20. Solitary Sandpiper (solsan)
21. Greater Yellowlegs (greyel)
22. Willet (willet1)
23. Lesser Yellowlegs (lesyel)

In order to request data from the eBird API, a county code is required in the format CC-SS-nnn, where CC = country code, SS = state code, and nnn = county FIPS code. For example, Atlantic County eBird county code is US-NJ-001. These strings were constructed programmatically in the script by leveraging data from the FCC ('https://transition.fcc.gov/oet/info/maps/census/fips/fips.txt') containing county and state FIPS codes web scraping techniques with beautifulsoup4. 

The primary datasets (eBird and NOAA CO-OPS) are constructed and merged in the NOAA_eBird_data_acquisition_cleaning_merging.py script. The output data is saved in the 'data' folder for each run and the file is saved using the date range used for data requesting. Because each run of the script only provides several weeks worth of data, a script was written to merge the datasets in the 'data' folder and save the consolidated dataset into the 'all_data' folder. The data can be updated using the 'weekly_data_load_join.py' file. Recommendation is to upload weekly due to frequency of NOAA data uploads. The NOAA_eBird_data_acquisition_cleaning_merging.py and weekly_data_load_join.py scripts should be run weekly over the course of months or years to continue growing the dataset. At time of construction, the dataset consists of 168 rows and the following columns:

1. sightingID
2. observationDate
3. observationTime
4. county
5. speciesName
6. speciesCode
7. locationName
8. locationID
9. lat
10. lng
11. howMany
12. tideStationName
13. highhighTime
14. highhighWaterLevel
15. highTime
16. highWaterLevel
17. lowTime
18. lowWaterLevel
19. lowlowTime
20. lowlowWaterLevel

For future iterations of this project, there are several opportunities for enrichment and expansion. For starters, there are additional datasets available for some tidal stations via the NOAA CO-OPS API, including seawater salinity, humidity, wind, air temperature, visibility, and water temperature. These values could potentially be integrated into the dataset to allow additional questions to be asked around relationship of environmental factors to avian sightings. Additionally, the extent of species being studied could be expanded. For this version of the project, only shorebirds were used. Other types of birds such as gulls, terns, and jaegers are also important birds which leverage the ocean shores of New Jersey as vital habitat, could be included in future iterations of the project. Additionally, there are tidal stations in other coastal and neighboring states including New York, Delaware, and Maryland that could be included in future revisions.



