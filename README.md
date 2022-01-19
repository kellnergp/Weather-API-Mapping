# Weather API Mapping

## Overview

This project uses the OpenWeather API to source weather data for hundreds of cities across the globe. 

The weather data is plotted to observe global weather trends and examine any possible correlations.

The data is then used to filter for locations with pleasant vacation weather and assemble a Google Maps figure with information concering potential hotel accomodations in select locations.

![hotelMap](/VacationPy/map.png)

## Tools Used

Python

OpenWeather API

Pandas

PyPlot

Gmaps

# Code Walkthrough

<details>
  <summary>Click to expand!</summary>

## WeatherPy

### Generate Cities List

First, use the provided code to generate a list of latitude-longitude pairs and use the CitiPy library to determine cities nearby each of the coordinate pairs.
Store city names into a list object for use later.

### Perform API Calls

Establish a variable to store the base url for calling the OpenWeather API.

Then, declare empty lists to store the max temperature, humidity, cloudiness, wind speed, country, and access date for each city.  Additionally, create lists to store the coordinates for each city in the API to have more accurate locations for processing.

Loop through every city in the list, using the city name to make an API call and temporarily store it as a .JSON file.

Use a try-except statement to append values for each city to the pre-made list objects, with the except statement accounting for a KeyError signifying the API doesn't have data for a given city by appending empty values for that city.

Print a log of the call attempt for each iteration with the city name and a counter that iterates each loop.

### Convert Raw Data to DataFrame

Before collating the data into a DataFrame, convert the max temperature data into Fahrenheit using the equation: "Temp (F) = (Temp (K) - 273.15) * (5/9) + 32.

Use a Pandas function to build a DataFrame with the city names, coordinates, max temp, humidity, cloudiness, wind speed, country, and date.

Then, remove cities lacking data with the dropna(axis=0, inplace=True) function.

Save the DataFrame to a csv file for use in the VacationPy section of the assignment.

Finally, use the Pandas .describe() function to check if there are any cities with a reported humidity value greater than 100%.  If there are, remove them.

## Plotting the Data

### Latitude vs. Temperature, Humidity, Cloudiness, and Wind Speed

Use the Pandas DataFrame.plot.scatter() function the generate plots with x-values of Latitude and y-values of Temperature, Humidity, Cloudiness, and Wind Speed each on their own plot.

Describe what each plot is showing.

Use proper plot labels, titles, and axes labels for each plot with the date of analysis included.

Save a png image of each plot to an output data folder.
  
  ![LatTempGraph](/WeatherPy/output_data/Fig1.png)

## Linear Regression

First, create two DataFrames representing the Northern and Southern Hemispheres by calling rows where latitude is greater than 0 and less than 0 respectively.

Repeat the 4 plots from the previous section, once each for both Hemispheres.

Use the scipy.stats.linregress function to take a linear regression of the data for each plot and use the determined values to plot the linear regression for each plot and annotate the regression line equation.

Print the r-value of each regression with its corresponding plot to illustrate how representative the regression is of any relationship between latitude and the observed data.

For each pair of regressions, describe what the plots are modeling and any trends present.
  
  ![northLatTempRegr](/WeatherPy/output_data/Fig5n.png)

## VacationPy

### Store Part I results into DataFrame

Use a Pandas function to read the csv file created in the WeatherPy section to a DataFrame.

### Humidity Heatmap

Configure gmaps using your google api-key.

Use gmaps functions to generate a world map figure.

Create a list object containing coordinate pairs from the DataFrame for each city.
Create another list containing the humidity values for each city.

Use the gmaps heatmap_layer function to create a heatmap with the locations in the list with the humidity values as the weight.

Add the heatmap layer to the figure and display the map.
Adjust figure size to display a single, proper map.

### Create new DataFrame fitting weather criteria

Generate variables storing ideal weather conditions for you, including minimum and maximum acceptable peak temperature, cloudcover percentage, and wind speed.

Create a new DataFrame, hotel_df containing only cities that contain max temp, cloudiness, and wind speed values falling within the criteria that were decided on previously.

### Hotel Map

Generate an empty list for storing hotel names.

Store the url for API calls to Google's nearby search API.

Loop through each city fitting the weather criteria making API calls looking for a hotel within 5000 meters of the city coordinates.

Use a try-except statement to append the hotel's name to the list.  If there is an IndexError, append an empty value.

Add the hotel names to the hotel DataFrame.

Drop any cities for which the API couldn't find a result with the dropna function.

Use the provided code to generate info-box content for each city and hotel.

Store the coordinates for each city with a hotel into a list object.

Use a gmaps function to create a marker layer with the hotel locations and info-box content.

Add the marker layer to the map figure and display it.

Save a screenshot of the final map with heatmap and marker layers.
  
  ![hotelMapPopup](/VacationPy/screenshot.png)
  
  </details>
  
## Contact

Galen Kellner: kellnergp@gmail.com
