# Mission-to-Mars

## Project Overview
The client, an aerospace company, wants information about Mars including any news about missions involving Mars and any information about the climate of Mars. All the desired information is collected from public websites using web scraping techniques.

## Resources

### Data Sources

- `https://redplanetscience.com` (Website containing Mars News)
- `https://data-class-mars-challenge.s3.amazonaws.com/Mars/index.html` (Website containing Mars Temperature Data)

### Software

- Python 3.9.13
- Jupyter Notebook 6.4.12
- Splinter 0.18.1
- Selenium 4.6.0
- Webdriver Manager 3.8.4
- Beautiful Soup 4.11.1
- PyMongo 4.3.2
- Pandas 1.4.4
- Numpy 1.21.5
- Matplotlib 3.5.2

Web scraping involves Beautiful Soup parsing HTML code. This requires the `html5lib` and the `lxml` libraries for Python.

## Web Scraping
Web scraping is done by using Splinter, Selenium, and the Webdriver Manager to set up the Splinter browser to run an automated Chrome browser to navigate to a desired website. Beautiful Soup then parses the HTML script of the page and then picks out specific elements as desired.

The first web scraping is conducted on the Mars News website (scripted in the former half of `mars_data_challenge_part_1.ipynb`). After parsing the HTML, the articles are scraped. The titles and article previews are extracted and placed into Python dictionaries; each dictionary represents an article with the title and preview. These dictionaries are stored in a Python list. This list is then dumped into a JSON string to be written to a JSON file, which can be used to import to a Mongo database (two methods of importing to MongoDB are demonstrated in the latter half of `mars_data_challenge_part_1.ipynb`). The program in the Notebook file was last run on November 17, 2022, so fifteen articles were scraped from the web page at that day.

The second web scraping is conducted on the Mars Temperature Data website (scripted in the first section of `mars_data_challenge_part_2.ipynb`). The HTML is parsed and scraped through two different methods. The first method uses Pandas to read through any HTML tables on a web page which are stored into a list of DataFrames. The other method uses the Splinter browser to parse and scrape the HTML with Beautiful Soup. The table header elements are extracted into a list of column labels, and the table data elements are extracted row by row; all are assembled into a DataFrame. Whichever method is used, the DataFrame has the data types adjusted to correctly reflect the contents.

The second section of `mars_data_challenge_part_2.ipynb` analyzes and processes the DataFrame to create some plots and answer some questions:

- How many months exist on Mars?
    - Looking at the Martian month column, the maximum value is `12`, so there are ***twelve months*** in one Martian year.

- How many Martian days' worth of data exist in the scraped dataset?
    - Looking at the sol (Martian day) column, the maximum value is `1,977` and the minimum value is `10`. The dataset started 10 sols in, and the last reading took place 1,977 sols in. Thus, the scraped dataset spans across ***1,967 sols (Martian days)***.

- What are the coldest and the warmest months on Mars (at the location of the Curiosity)?
    - The daily minimum observed temperature values are grouped by month, averaged, and then plotted in the bar chart below. As shown, _the coldest month is **Month 3** with an average temperature of **-83.3073 &deg;C**_, and _the warmest month is **Month 8** with an average temperature of **-68.383 &deg;C**_.
![Average temperature on Mars by month](https://github.com/Owen-Wang1234/Mission-to-Mars/blob/main/monthly_temp.png)

- What months have the lowest and the highest atmospheric pressure on Mars (at the location of the Curiosity)?
    - The daily observed pressure values are grouped by month, averaged, and then plotted in the bar chart below. As shown, _the lowest pressure is observed in **Month 6** with an average pressure of **745.054 Pascals**_, and _the highest pressure is observed in **Month 9** with an average pressure of **913.306 Pascals**_.
![Average pressure on Mars by month](https://github.com/Owen-Wang1234/Mission-to-Mars/blob/main/monthly_press.png)

- About how many terrestrial days exist in a Martian year?
    - The daily minimum observed temperature is plotted over time to discern a pattern in the temperature as Mars orbits the Sun. As shown below, there appears to be about three Martian cycles over the span of about 5.5 terrestrial years (and one of those years is a leap year). This implies that one Martian year is calculated to be about **669.5 Earth days**.
    - The Mars Facts website (`https://galaxyfacts-mars.com`) states that one Martian year is about **687 Earth days**, so the error ends up being about **-2.55%**.
![Daily temperature on Mars](https://github.com/Owen-Wang1234/Mission-to-Mars/blob/main/daily_temp.png)

The last section of `mars_data_challenge_part_2.ipynb` exports the DataFrame into a CSV file, and, as an extra feature, shows how to import to a Mongo database (both methods used in `mars_data_challenge_part_1.ipynb` are demonstrated here as well) and explore the data through MongoDB.