# Analysis of Weather and Vacation Data using APIs


## General Overview

This was an assignment I completed for the Northwestern Data Science and Vizualization Bootcamp. I received an A.

I used Jupyter Notebook to extract weather and vacation data from APIs.

### Weather Data

Weather data was extracted from [openweathermap.org](https://api.openweathermap.org). Data from each API request was converted to a json object.
Below are the general project steps.

1. Generated a list of cities: Looped through a list of over 600 latitude-longitude pairs to find the nearest city using citipy.
2. Performed a weather check on each city using a series of successive API calls; saved weather data for each city in lists.
3. Created pandas dataframe from lists and exported dataframe to a CSV file to be used on the vacation data.
4. Analyzed the relationships between latitude and weather with scatterplots and linear regression.

        Code snippet:
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
