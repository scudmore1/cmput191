# Data Analysis of Global Fresh Bread Prices - Haley, Simon, & Tomas
CMPUT 191 (FALL 2024) - Assignment 3

## Synopsis

To effectively analyze the concept of purchasing power parity, we conducted an extensive analysis of fresh bread prices worldwide. During the product selection process, we aimed to choose a product near the origin of the food production process with high liquidity to isolate additional processing costs and market inefficiencies. As a result, we landed on fresh bread (500 grams) for our analysis and used the a mix of developed and developing countries in our dataset.

For our analysis, we deployed a 14-step process to get from raw data to insights:

### step 1: scrape data on fresh bread pricing from Numbeo
This involved web scraping our data usinng requests.get, BeautifulSoup, find, as well as the scrape_table variable to pull necessary data. We found the latest pricing on fresh bread at a standardized unit of 500 grams.

### step 2: data cleaning
Data cleaning involved using the sort function (to organize our list of countries) and the take & np.arange functions together to pull 10 countries from the list. This list included a list of developed and developing countries. 

### step 3: scrape country codes from CurrencyScoop
This also involved web scraping our data usinng requests.get, BeautifulSoup, find, as well as the scrape_table variable to pull necessary data. 

### step 4: display currencies on each country
Using our exchange rate data collected for our list of countries on 2024/11/29, we put the exchange rates and the currency code for each country into a dictionary that we could use to build into our dataset. Then we used the apply and lambda functions to iterate through our data and divide the raw price by the exchange rate to get the Local Price. Additionally, we combined the apply and lambda functions again to get add a column into our table that showed the currency code for each country. We did this step to show the local prices of fresh bread since the dataset already had converted it into CAD.

### step 5: diplaying the data using a bar chart
First, we imported our CAD-converted pricing data into an array, then calculated the price differential compared to Canada using the loc and values functions to select Canada's row and take the first value in the index. Next, we  created a new column that contained data for the price differences (CAD price in each respective country - CAD price for Canada) to get a spread of values showing how much more/less they charge. After this, we used the plt.bar function to display the values. 

![image](https://github.com/user-attachments/assets/b4474c24-0baa-4457-9808-ac51f50268e3)

## External Factor Analysis

To effectively analyze the price differential between fresh bread prices across the world,
we elected to use national imports of fresh bread as our external factor due to the material effect of supply on the price of the commodity. While we considered the potential impact of population size differentials, the size of the country’s financial sector (as an indicator of economic development), and the impact of transportation costs for our external factor, we selected national imports due to the strong influence of global trade movements on commodity prices. Within our hypothesis, we expected that the largest national importers of fresh bread would be able to access the product at a lower cost, and in theory, should have a lower price compared to peer countries.

## Concluding Analysis

After a comparative analysis of fresh bread prices across Norway, South Korea, Austria,
Luxembourg, Austria, Canada, Sweden, the United States, Costa Rica, and Denmark, we identified three primary conclusions: purchasing power parity does not hold for fresh bread prices and the use of national imports does not prove to be a statistically significant explanatory variable for fresh bread price determination. Given the low correlation of 0.307 and insignificant p-value of 0.387 from our analysis, we conclude that national imports are not an accurate indicator of increases or decreases in local fresh bread prices. When analyzing the data on fresh bread, we found wide dispersion between countries with high imports and their respective prices for the product. South Korea was one of the largest importers of fresh bread in our dataset, yet its prices were very close to the mean. Moreover, Switzerland had near-average national imports compared to peers but had the highest pricing in our dataset. This variation could be due to differing demand levels, tariffs, population differences, and varying local production levels. On the contrary, we found that Sweden had the lowest product price, only below Canada which similarly had a low cost relative to peers. This is primarily due to local production supplying the bulk of Canada’s grain demand and lower relative tariffs for Sweden given that they are a part of the European Union which allows them to import grain products with no additional tariff, unlike Switzerland. After further analysis, we identified that the higher prices of food products in Switzerland were not exclusive to fresh bread; Switzerland is the second most expensive country on the Numbeo Grocery Index for 2023, pointing to additional factors such as high labor costs, lower accessibility of substitutes, and higher duties levied on select food products (Numbeo, 2023). In conclusion, we found that purchasing power parity does not hold for fresh bread across the world, and a multitude of factors contribute to the wide differentials between countries.
