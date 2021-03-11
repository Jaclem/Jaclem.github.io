## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/Jaclem/Jaclem.github.io/edit/main/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Python

Final Project: Build a webscraper that scrapes specific information of your choice from a website of your choice and puts it into a CSV file.
For my project I decided to use BeautifulSoup for the web scraping 
I also added a webdriver using selenium to open up the chrome web browser and take user input and automatically click on the first option after it is entered into the site search bar. It then would scrape all the information of the Alltrails website and write it into a CSV file.
```
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from bs4 import BeautifulSoup
import urllib.request
import csv
import time

# Opening chrome browser using selenium
browser = webdriver.Chrome("F:\Program Files\chromedriver_win32\chromedriver.exe")
browser.get('https://www.alltrails.com/')
# Sleeping for 5 seconds to allow time for page to open
time.sleep(4)

# Finds direct path to Cookie pop-up 'decline' button and clicks on it
cookie = browser.find_element_by_xpath('//*[@id="page-home-index"]/div[2]/div/a[1]')
cookie.click()


# Finds the alltrails search by xpath and clicks on it
search = browser.find_element_by_xpath('//*[@id="home-search"]')
search.click()

# Takes user input and types it into search bar
userSearch = str(input("Please enter a city ")).capitalize()
search.send_keys(userSearch)

time.sleep(2)
# Clicks on suggested path
userGeneratedSearch = browser.find_element_by_xpath('//*[@id="hits"]/div[1]')
userGeneratedSearch.click()


time.sleep(2)
pageClick = browser.find_element_by_xpath('//*[@id="content"]')
pageClick.click()

time.sleep(3)

URL = browser.current_url

# Creating variable html_doc to be saved as and opened by the url library module
html_doc = urllib.request.urlopen(URL)

# soup variable parsing html from html_doc variable
soup = BeautifulSoup(html_doc, 'html.parser')


def writeFile(self):
    f = open('trails.csv', 'a')
    f.write(self + '\n')
    f.close()


def fullHeader():
    # Saving full contents of div that has page header 'Top Trails (#_of_trails)'
    header = soup.find(class_='col-lg-4 col-md-4 col-sm-12 col-xs-12')
    top_trails = header.h3.a.text.replace(',', '')

    writeFile(top_trails + ',' + 'for ' + userSearch)

def categoryList():
    categories = ["Trail Name", "Difficulty", "Distance"]
    # joins together the separate categories with a comma
    comma_seperated_categories = ','.join(categories)


    writeFile(comma_seperated_categories)

#--------------------------------------------#
# Calls the first two functions that write the headers
fullHeader()
categoryList()

#--------------------------------------------#

trail = soup.find_all('div', attrs={'class':'styles-module__container___10uYZ'})

for trails in trail:
    trails = trails

    # Finds the div that contains all of the needed information
    info_container = trails(class_='styles-module__content___1eARw')
    # In the first container of every container find the itemprop 'name' which is the item name
    itemprop = info_container[0](itemprop='name')
    # Trail name in text form with comma's deleted
    title = itemprop[0].text.replace(',','')

    #--------------------------------------------#

    difficulty = info_container[0].span.text

    #--------------------------------------------#

    # Finds all containers of type span with a class xlate-none which has the length
    length_container = trails('span', attrs={'class':'xlate-none'})
    distance = length_container[0].text.strip('Length: ')

    #--------------------------------------------#

    writeFile(title + ',' + difficulty + ',' + distance)
```
```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Jaclem/Jaclem.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
