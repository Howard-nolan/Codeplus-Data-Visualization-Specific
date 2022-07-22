# Visualizations

### Stacked Bar Graph of Tank Types per State
This visualization cleanly displays the distribution of the different types of tanks for every state through a stacked bar chart. For each state, there is a color coded breakdown of tank type. There is also a key at the top right corner indicating which color correlates to which tank type.
This visualization is helpful if you want to look at the different tank types that are popular or unpopular within a state. 
To make this visualization, we use the tank ast data and calculate the number of tanks in each state by the tank type. Afterwards, we converted the dataframe to a pivot table which contains the number of each type of tank in each state. Then, we used matplotlib to create a stacked bar plot out of that pivot table.

<img src="/images/01_stacked_bar.PNG" alt="flowchart" width="500"/>


### Number of Children Per County
This map is a non-gpu visualization that shows a breakdown of the US by county, with each county being shaded differently based on the number of total children within that county. To make this visualization, we read in the preprocessed data frame that includes the calculated number of children per county and also geometries of each county in the US. In this visualization, we also plotted the tanks over the county breakdowns. To do so, we separately plot the tanks, before overlaying the tanks on top of the map with the county breakdowns. You can do this using the ```*``` operator, which in essence overlays one geoviews map on top of another.

![Gif](images/02_children_per_county.gif)


### Map Colored by Number of Households Within 5mi of a Tank
This map is a non-gpu map that is shaded by the number of households within 5mi of a tank. This is helpful because the user can look at which counties have more households closer to tanks, which is important in identifying which areas are in potential risk zones if a petrochemical tank does spill. 
We made this visualization using the geoviews library by plotting the geometries of the counties in the US shaded by the number of households within 5mi of a tank. We also plotted the tanks and then overlaid the tanks map on top of the map with the US counties using the ```*``` operator.

![Gif](images/03_hh_per_county.gif)

### Charleston County Case Study
This Charleston County visualization is a gpu cuxfilter dashboard with a zoom in of all of the households and tanks in Charleston County plotted on a map. On the sides of the dashboard, there are multi select features to display whether or not a household contains elderly people and whether or not households are within a certain distance range of a tank. We also included a distance range slider so that users can look at households a specific distance range away from a tank.

To create this case study visualization, we first imported the pre-processed file with distances between each household in Charleston and its nearest tank. This file also had the tank coordinates and household coordinates already merged together in one column, allowing for the coordinates to plot onto one cuxfilter dashboard. When plotting these charts, you can specify different colors for the points that represent households, and the points for tanks. To do so, we made a separate column classifying whether or not that point was a tank or a household ```is_tank``` using 0 and 1’s. By specifying that column in the ```aggregate_col``` parameter, the colors of the points will be different, and provide clarity as to whether the points are tanks or households. We also made multi select features through specifying the feature, its parameters, and plotting them alongside the main map.


![Gif](images/04_charleston_dist.gif)

### Harris County Case Study
For this visualization, we took the same steps as the ones described above, the exception being that we used a different pre-processed file with households in Harris County. Our output visualization also contains the same multiselect and sliding features as the Charleston County case study map.

![Gif](images/05_harris_dist.gif)


### Map of All US Households Plotted and Colored by Distance to Nearest Tank
This visualization is also similar to the ones mentioned above. Here, we have a map of the United States with all of the households that have elderly and children plotted. We also have all the tanks plotted in a different color as well. On the side, we have the elderly age category multiselect and the distance to tanks range slider.

![Gif](images/06_all_us_dist.gif)


### Maps of All US Households Colored by Distance to Nearest Tank with Natural Hazard Sliders
These visualizations display a map of the US with all households containing elderly and children as well as all of the tanks in the US. On the side, there is a natural hazard risk range slider for a specific risk. We thus have made these visualizations for each of the 6 natural hazard risks: hurricanes, earthquakes, tornados, strong wind, coastal flooding, and riverine flooding. These range sliders allow users to look at households with a specific risk index to a certain natural hazard. We also have included the distance range slider so that users can also look at households a specific distance range away from a tank. This is helpful because tanks and households close to each other will oftentimes be associated with the same risk index. 

To make these 6 separate visualizations, we first read in the pre-processed file that contained household and tank coordinates, as well as risk indexes for each of the 6 risks. Then, since we wanted to plot each of the risks separately, we made separate dataframes with the household and tank coordinates along with one of each of the risk columns. To make each of the individual visualizations, we would read in one of the dataframes, convert them to cuxfilter data frames, specify the multi select and range slider parameters, before plotting them onto a dashboard. 

![Gif](images/07_coastal_flooding_data.gif)

### Address Lookup Web App
This is a web app that allows users to type in an address anywhere in the US, and the web app will output how far away (in miles) the nearest petrochemical tank is from the input location. The natural disaster risk index of the nearest location will also be displayed on the screen along with a detailed zoomed in map of the input location and the ten closest tanks. 
We are using the Folium library to visualize the zoomed in map, current location markers, and ten nearest tanks markers. Once the input address is inputted into the search bar, we are using the Open Map Street and Google Maps geocoding api to convert the address to latitude and longitude coordinates. This web app is hosted on a virtual machine run by Oracle.

<img src="/images/12_webapp1.gif" alt="flowchart" width="500"/>
