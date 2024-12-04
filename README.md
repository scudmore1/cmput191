# Data Analysis of Global Fresh Bread Prices - Haley, Simon, & Tomas
CMPUT 191 (FALL 2024) - Assignment 3

## Synopsis

To effectively analyze the concept of purchasing power parity, we conducted an extensive analysis of fresh bread prices worldwide. During the product selection process, we aimed to choose a product near the origin of the food production process with high liquidity to isolate additional processing costs and market inefficiencies. As a result, we landed on fresh bread (500 grams) for our analysis and used the a mix of developed and developing countries in our dataset.

For our analysis, we deployed a 14-step process to get from raw data to insights:

### step 1: scrape data on fresh bread pricing from Numbeo
This involved web scraping our data using requests.get, BeautifulSoup, find, as well as the scrape_table variable to pull necessary data. We found the latest pricing on fresh bread at a standardized unit of 500 grams.

### step 2: data cleaning
Data cleaning involved using the sort function (to organize our list of countries) and the take & np.arange functions together to pull 10 countries from the list. This list included a list of developed and developing countries. 

### step 3: scrape country codes from CurrencyScoop
This also involved web scraping our data using requests.get, BeautifulSoup, find, as well as the scrape_table variable to pull necessary data. 

### step 4: display currencies on each country
Using our exchange rate data collected for our list of countries on 2024/11/29, we put the exchange rates and the currency code for each country into a dictionary that we could use to build into our dataset. Then we used the apply and lambda functions to iterate through our data and divide the raw price by the exchange rate to get the Local Price. Additionally, we combined the apply and lambda functions again to get add a column into our table that showed the currency code for each country. We did this step to show the local prices of fresh bread since the dataset already had converted it into CAD.

### step 5: diplaying the data using a bar chart
First, we imported our CAD-converted pricing data into an array, then calculated the price differential compared to Canada using the loc and values functions to select Canada's row and take the first value in the index. Next, we  created a new column that contained data for the price differences (CAD price in each respective country - CAD price for Canada) to get a spread of values showing how much more/less they charge. After this, we used the plt.bar function to display the values. As demonstrated below, Switzerland, USA, and Denmark had the largest positive differentials comparatively, while Sweden had the least relative to Canada. Also, Canada sat near the bottom of our dataset, demonstrating very cheap pricing compared to peers.

![image](https://github.com/user-attachments/assets/b4474c24-0baa-4457-9808-ac51f50268e3)

### step 6: importing data on an external factor
Similar to the above datasets, we employed requests.get, BeautifulSoup, find, as well as the scrape_table variable to pull necessary data. We pulled our data from IndexMundi on national imports of wheat products globally as a proxy for bargaining power for fresh bread. To clean this data, we dropped columns that contained error messages, using the drop function, and selected only the 10 desired countries from our original dataset using the isin function which referenced an array with the countries we wanted.

### step 7: importing more data since EU imports were bulked together
To get import data on all the countries we needed, we also web scraped data from the World Bank's website, specifically for Denmark, Luxembourg, Austria, and Sweden. We added this into our table using the concat function.

### step 8: data cleaning our new table 
Before joining this data into our existing table with exchange rates, we used the strip function (to check for any extra white spaces in the data) and used an if statement to verify that each country name matched that of the other table. 

### step 9: add the price differential table into this table which has the exchange rate and imports data
Next, we used the merge function to build in our price differentials data to this combined dataset, which now contains all the necessary information we need.

![image](https://github.com/user-attachments/assets/baa05547-86ca-4c46-93d3-c09418b1403e)


## External Factor Analysis

To effectively analyze the price differential between fresh bread prices across the world,
we elected to use national imports of fresh bread as our external factor due to the material effect of supply on the price of the commodity. While we considered the potential impact of population size differentials, the size of the country’s financial sector (as an indicator of economic development), and the impact of transportation costs for our external factor, we selected national imports due to the strong influence of global trade movements on commodity prices. Within our hypothesis, we expected that the largest national importers of fresh bread would be able to access the product at a lower cost, and in theory, should have a lower price compared to peer countries.

### step 10: compare data on price differential to imports through bar charts
Now to visually compare our external factor we built two bar charts for our data. Off the bat, we noticed that imports did not seem to match up with pricing...

![image](https://github.com/user-attachments/assets/43bb81c1-ddec-40f2-80e6-81873efac02e) ![image](https://github.com/user-attachments/assets/b071bc72-8d41-4580-95cd-8da538dfef57)

### step 11: analyzing wheat prices directly to see relationship with wheat imports
First we took the current wheat price from Business Insider on 2024/11/29 at 8:52PM MT, then we took the USD exchange rates from exchange-rates.org; using the rates we collected, we assigned them to an array containing our selected countries and made a new table that matched each country with their respective exchange rates.

### step 12: getting exchange rates for CAD from the Bank of Canada
To compare wheat prices with pricing in local currency, we similarly pulled exchange rate data from the Bank of Canada and added it to our table. To get wheat import cost estimates, we multiplied the cost of wheat in CAD/MT by the amount of wheat imports in thousands of MT. 

### step 13: creating a scatter plot with fresh bread prices and wheat import costs
We plotted the CAD pricing of fresh bread against the wheat import costs in CAD

![image](https://github.com/user-attachments/assets/b981b7d3-8ede-4d13-92e1-24b2264bad77)
![image](https://github.com/user-attachments/assets/cceab1b6-7ea5-43bd-b70d-0230b5ec812f)

### step 14: calculate the correlation and p-value
Using the correlation and p-value pre-built variables, we calculated a correlation of 0.307 and a p-value of 0.387


## Concluding Analysis

After a comparative analysis of fresh bread prices across Norway, South Korea, Austria,
Luxembourg, Austria, Canada, Sweden, the United States, Costa Rica, and Denmark, we identified three primary conclusions: purchasing power parity does not hold for fresh bread prices and the use of national imports does not prove to be a statistically significant explanatory variable for fresh bread price determination. Given the low correlation of 0.307 and insignificant p-value of 0.387 from our analysis, we conclude that national imports are not an accurate indicator of increases or decreases in local fresh bread prices. When analyzing the data on fresh bread, we found wide dispersion between countries with high imports and their respective prices for the product. South Korea was one of the largest importers of fresh bread in our dataset, yet its prices were very close to the mean. Moreover, Switzerland had near-average national imports compared to peers but had the highest pricing in our dataset. This variation could be due to differing demand levels, tariffs, population differences, and varying local production levels. On the contrary, we found that Sweden had the lowest product price, only below Canada which similarly had a low cost relative to peers. This is primarily due to local production supplying the bulk of Canada’s grain demand and lower relative tariffs for Sweden given that they are a part of the European Union which allows them to import grain products with no additional tariff, unlike Switzerland. After further analysis, we identified that the higher prices of food products in Switzerland were not exclusive to fresh bread; Switzerland is the second most expensive country on the Numbeo Grocery Index for 2023, pointing to additional factors such as high labor costs, lower accessibility of substitutes, and higher duties levied on select food products (Numbeo, 2023). In conclusion, we found that purchasing power parity does not hold for fresh bread across the world, and a multitude of factors contribute to the wide differentials between countries.
