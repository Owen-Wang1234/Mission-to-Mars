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
- Matplotlib 3.5.2

Web scraping involves Beautiful Soup parsing HTML code. This requires the `html5lib` and the `lxml` libraries for Python.

## Web Scraping
Web scraping is done by using Splinter, Selenium, and the Webdriver Manager to set up the Splinter browser to run an automated Chrome browser to navigate to a desired website. Beautiful Soup then parses the HTML script of the page and then picks out specific elements as desired.

The first web scraping is conducted on the Mars News website (scripted in the former half of `mars_data_challenge_part_1.ipynb`). After parsing the HTML, the article are scraped. The titles and article previews are extracted and placed into Python dictionaries; each dictionary represents an article with the title and preview. These dictionaries are stored in a Python list. This list is then dumped into a JSON string to be written to a JSON file, which can be used to import to a Mongo database (two methods of importing to MongoDB are demonstrated in the latter half of `mars_data_challenge_part_1.ipynb`). The program in the Notebook file was last run on November 17, 2022, so fifteen articles were scraped from the web page at that day.

The second web scraping is conducted on the Mars Temperature Data website (scripted in `mars_data_challenge_part_2.ipynb`).