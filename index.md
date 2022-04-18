# **Housing Price Change**
## *Python Application displaying Percentage Change in Housing Prices from 2010-2019*
### Enter a State (capitalized) to get started!
<iframe src="https://house-price-choro.herokuapp.com/" height="570" width="100%" frameBorder="10"></iframe>

This application (above) is a collection of Python Scripts myself and my colleagues have made to visualize trends in the US real estate market. The pricing information was gathered from data made publicly available from Zillow, and the population information was gathered from the US census. These data sets were cleaned and merged to compute percentage changes (both year-on-year and aggregated for the decade) at the state and county level (done mostly with base Python and Pandas). Then using Plotly, we visualized these trends using choropleth maps. Finally, we turned these Python scripts into a webapp using Dash, and hosted them using Heroku to display on this Github Pages site.  
*(The choropleths, especially the median house price ones, do take a while to load as they have to render a lot of data using the relatively low-load system provided to us by Heroku. The app runs slightly faster [on its own](https://house-price-choro.herokuapp.com/) if you'd like to see for yourself)*  

This project was primarily an exercise in data engineering and visualization. The full project, as well as steps to recreate it can be found in [the GitHub Repository](https://github.com/amal-kadri/Housing_Price_Choropleth_app), or using the button at the top of the page!

![ChoropletGif1](docs/assets/choropleth-gif-1.gif)

## Collaborators:  
Amal Kadri: [https://github.com/amal-kadri](https://github.com/amal-kadri)  
Parker Gauthier: [https://github.com/parkergauthier](https://github.com/parkergauthier)  
Jonathan Bowman: [https://github.com/bowman-jonathan](https://github.com/bowman-jonathan)  
Elle Boodsakorn: [https://github.com/khun-elle](https://github.com/khun-elle)  
Haokun Zhang: [https://github.com/haokunz](https://github.com/haokunz)  
Kevin O’Connor: [https://github.com/k-oconnor](https://github.com/k-oconnor)  
Karlo Vlahek: [https://github.com/KarloVlahek](https://github.com/KarloVlahek)

**At the time of making this website (04/18/2022) Heroku's Integration with GitHub was not functioning properly, so the app was published manually through the Heroku CLI. This should hopefully not be an issue going forward, and we recommend using GitHub version control for collaboration going forward. This is only an issue with the webapp hosting, and not with the core functionality of the apps themselves or the underlying code.*
