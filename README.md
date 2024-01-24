# Tacos_-and_Burritos

## Overview

### Simple analysis of scraped taco and burrito menu prices by state, including data cleanup in Python, simple statistical analysis of outliers, visualization in Tableau.

## Results

Visualizations created in Tableau can be seen here: [Tacos and Burritos](https://public.tableau.com/views/Tacos_17052880305940/Dashboard1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)

## Method

The original dataset was downloaded from Data.World and can be found here: [Restaurants That Sell Burritos and Tacos in the US](https://data.world/datafiniti/restaurants-burritos-and-tacos)

The data was scraped from online menus according to the criteria that the menu item has the word 'Taco' or 'Burrito' in it. The initial dataset was approximately 77,000 rows and included fields related to restaurant name, menu item name, pricing, description, etc.

### Cleanup

The included notebook contains the cleanup steps. I knew that I wanted to create a map visualization of the average price of a taco and a burrito respectively for each state. So the first cleaning step was to remove any rows with nulls in the price field or in the state/province field. This left me with about 27,000 rows, so still plenty to create my visualization.

Next I pulled the string 'Taco' and 'Burrito' from the item name to create a new 'Type' column that simply differentiated 'Taco' and 'Burrito'. I would use this field to separate the data according to type in Tableau. A simple value count showed I had about 15,000 rows of tacos and 11,000 rows of burritos.

I then used Plotly to plot a normal distribution of the pricing data to get a sense of how the data was distributed. WIth the exception of a few outliers ($1300 for a taco??) the data was relatively normal. Therefore I decided to use a simple 3-sigma rule to exclude outliers, which was done using the Statistics library.

I then saved the cleaned up dataframe to a new csv file.

### Vizualization

There were a few more manipulations of the data I chose to do in Tableau. First, the state/province field was a mix of two letter state abbreviations and long province names as well as some other random data. To clean this up I created a calculated field using the following code:

[calculated_field](calculated_field.png)

This is just a snapshot but the code created a new calculated field where only the rows that had a state abbreviation were included and that abbreviation was transformed into the full state name. This would allow me to use the State datatype in Tableau to easily generate the interactive map.

Next I simply used the map function in teableau to plot the average price for tacos and burritos. I also made some tables to include in the dashboard, such as average minimum and maximum price by state.


