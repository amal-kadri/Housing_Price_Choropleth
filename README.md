# Housing_Price_Chloropleth
This is a website built using GitHub Pages to display our Housing Price Variation Project

this is our webpage: https://amal-kadri.github.io/Housing_Price_Choropleth_app/

the app itself is here: https://house-price-choro.herokuapp.com/

## Example Outputs
![ChoropletGif1](docs/assets/choropleth-gif-1.gif)
![Idaho-Yearly-Median-Price](docs/assets/idaho-yoy-median-price.gif)

## Instructions - How to use this code

### Preliminary: 
In terminal, change directory to the project folder Housing_Price_Chloropleth with command: "cd Housing_Price_Chloropleth" then run import required modules by running "pip install -r requirements.txt"

### Step 1: 
In bash, run command "python3 STEP1_CLEAN.py" to clean and merge the Zillow and Census data into pricing data

### Step 2: 
In bash, run command "python3 STEP2_FIPS.py" to merge the FIPS with the pricing data

### Step 3: 
In bash, run command "python3 STEP3_CTYFIPS.py" to merge the pricing data with geojson data

### For animated average weighted real estate price for all US states from 2010-2019: 
In bash, run command "python3 state_price.py"

### For percent change in 2010 price of average real estate price for all US states in 2019: 
In bash, run command "python3 state_percent_change.py"

### For animated average real estate price for a single state from 2010-2019: 
In bash, run command "python3 county_price.py", then respond to the prompt in bash with the US state of interest with the first letter capitalized.

### For percent change in 2010 price of average real estate price for a single state in 2019: 
In bash, run command "python3 county_percent_change.py", then respond to the prompt in bash with the US state of interest with the first letter capitalized.

## Overview
The objective of this project was to visualize percent change in average real estate prices on nation wide and state wide choropleth maps from 2010 to 2019. Percent change was measured on a year to year basis as well as total percent change accrued during the decade from a base line year (2010). Presenting the data in this way would allow an intuitive view of real asset growth in the United States, with the option of "zooming in" to the state level to see which counties drove those price changes.

## Data Description
Two separate datasets were needed to accomplish the descriptive analysis. The first was a list of housing prices with accompanying state, county and monthly pricing information, which was downloaded from Zillow, https://www.zillow.com/research/data/. The second was a list of yearly population estimates on both the state and county level, which was procured from the US Census website, https://www.census.gov/data/datasets/time-series/demo/popest/2010s-counties-total.html#par_textimage_70769902. 

## Data Limitations
The greatest limitation in the data is the lack of price observations for certain counties in the earlier years of the Zillow dataset. For certain states like South Dakota or Mississippi, numerous counties had no observations up to as late as 2017, which is likely due to a combination of Zillow being an emerging platform for real estate listings in the early 2010s and a lack of listings in general, as missing data often comes from less populous states. This absence will likely cause large swings in the percent change due to relatively fewer data points. The census data was comprehensive, though each year was a population estimate since the census is only taken every ten years. The study was limited to 2010-2019 due to way the census data is stored and recorded, however the missing data issue with the Zillow data from they time frame would have been even more acute. 

## Data Cleaning
Using a combination of pandas, base python, and numpy, census data was cleaned such that each row contained a single observation (a population for a given state/county/year). Using the state population estimate for a given year, the proportion of the state's population, for a given county, for a given year, was measured. The Zillow data was cleaned and grouped such that each row contained a single observation (an average price for a given state/county/year). 

## State Level Aggregation
Using the state, county, and year as a key, the datasets were joined. Using the state population proportion, each county's price was weighted to represent the relative number of people affected by that price. This weighted price was summed by state to get the weighted average price of real estate for a state in a given year. Using this weighted price the percent change in price was calculated from year to year, and cumulative percent change in price from the 2010 baseline price.

## County Level Aggregation
For the county level data, each observation was already grouped with the merged datasets. Additionally, since the objective was to get the percent price change within a county, percent change on the county level was calculated with the average price, not the price weighted by the state population. The percent change was calculated between the average real estate prices for counties from year to year and the cumulative percent change in price from the 2010 baseline price.

## Choropleth Preparation
Additional datasets were required to take the aggregated information and display it in choropleth maps. geojson files which contained latitudinal and longitudinal data representing the coordinates for counties and states were used in conjunction with the plotly package to draw counties and states on a blank map of the US, which. Additionally a FIPS data set which encoded the state and counties into numeric codes was used as an intermediary to join the aggregate price data and the geographic coordinates, which. The FIPS was joined to the pricing data on the state and county fields, and the resulting dataset was then joined to the geographic data via the FIPS code field. From that aggregated data frame a choropleth map could be generated using the choropleth package.

## Choropleth Visualization
Four separate choropleth maps scripts were generated for the data. For the continental US, an animated map was generated to show weighted price in real estate, where darker shades indicated a larger weighted price. An additional map was generated which displays the total percent change in the price from the 2010 baseline, where darker shades indicated a larger percent increase. For each US state, an animated map was generated to show absolute average real estate price for each county, where darker shades indicated a larger price increase. An additional map was generated which displays the total percent change in the price from the 2010 baseline, where darker shades indicated a larger percent increase. 

## Findings
As expected, the cumulative percent change in Mississippi and South Dakota was over 100 percent, however the massive number of missing observations for many counties in these states belies the reliability of these figures. States with large economies, like New York and California put up numbers in price levels, but percent changes were on par with other growing states like Colorado. Hawaii maintained as the state with the most expensive real estate through this period edging out California by 37 thousand, but upon inspection of the percent change from 2010, California's real estate prices have increase by over 71% compared to Hawaii's 42%, so it is likely that California will surpass Hawaii within the next 10 to 20 years. The states with the largest percent change in housing prices with reliable data was Idaho and Nevada. This could be due to Californians migrating to the states, causing an increase in demand for housing and therefore price. The slowest growing region of US house prices was the north east, with no state growing over 40% of their 2010 levels. This could indicate market saturation for the region and a correction from the 2008 financial crisis.

## Further Study
One potential avenue for more precise analysis could be to alter how the statewide population prices were weighted. The prices in this study are weighted by the proportion of the state populations, but another aspect real estate pricing relates to how populous a state is compared to the country as a whole. A certain county could be weighted heavily based on the proportion of state population that lives there, but could be in a relatively less populated state, distorting the relevancy of that price with a larger proportion of a smaller number of people than a more populous state. Considering Idaho and Nevada's growth, one useful metric might be tracking of migration to and from states to test whether our explanation of these regions growth is true. With the data we have, another avenue for exploration is to incorporate predictive analysis into our pricing percent changes and forecast the upcoming percent changes for the next decade. This could be achieved either through linear modeling or non linear KNN modeling using machine learning.
