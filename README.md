# Analysis of Weather using APIs


## General Overview

For WeatherPy, I used Jupyter Notebook, a weather website API, and pandas to create a csv file of weather data for over 600 cities. I investigated relationships between latitude and different weather patterns using scatterplots and regression. Using the data generated from WeatherPy, for VacationPy I created a map showing visual differences in humidities for each city. Finally, I added hotel locations for cities with good weather to the map.

### WeatherPy

Weather data was extracted from [openweathermap.org](https://api.openweathermap.org). Data from each API request was converted to a json object. Below are the general project steps.

1. Generated a list of cities: Looped through a list of over 600 latitude-longitude pairs to find the nearest city using citipy.
2. Performed a weather check on each city using a series of successive API calls; saved weather data for each city in lists.
3. Created pandas dataframe from lists and exported dataframe to a CSV file to be used on the vacation data.
4. Analyzed the relationships between latitude and weather with scatterplots and linear regression.

          def regression(x, y, x_label, y_label, hemisphere):
              title = f'{hemisphere} Hemisphere:\nRegressing {y_label} on {x_label}'
              (slope, intercept, rvalue, pvalue, stderr) = linregress(x, y)
              regress_values = x * slope + intercept
              line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
              plt.scatter(x, y)
              plt.plot(x,regress_values,"r-")
              plt.xlabel(x_label)
              plt.ylabel(y_label)
              plt.title(title)
              title = title.replace(':\n', '_').replace(' ', '_')
              plt.savefig(f'output_data/{title}.png')
              plt.show()
              print(line_eq)
              print()
              print(f"r = {pearsonr(x, y)[0]:.2f}, p = {pearsonr(x, y)[1]:.4f}, r_squared = {rvalue**2:.2f}")
              print()
      
![Example of Regression Output](/WeatherPy/output_data/Northern_Hemisphere_Regressing_Max_Temperature_(F)_on_Latitude.png)

![Example of Regression Interpretation](/WeatherPy/output_data/Interpretation_NH_Temp_Latitude.PNG)


### VacationPy

Created a heatmap with [Google Maps Platform](https://maps.googleapis.com) and csv file generated from WeatherPy code ("cities.csv").
Added markers on top of humidity heatmap that showed the nearest hotel within 5,000 meters to each city that was identified as having excellent weather.

Below are the general project steps.

1. Loaded cities.csv data into a pandas dataframe.
2. Used gmaps to create a heatmap showing the degree of humidity levels for each city.
3. Created new dataframe of cities with great weather conditions.
4. Looped through each city to identify the nearest hotel within 5,000 meters.
5. Added the hotel locations on top of the humidity heatmap.

![Hotel Map](/VacationPy/output_data/hotel_map.png)


