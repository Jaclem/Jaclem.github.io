# Python | <a href="https://Jaclem.github.io/SQL">SQL</a> | <a href="https://Jaclem.github.io/c programming">C Programming</a> | <a href="https://Jaclem.github.io/linux">Linux</a> | <a href="https://Jaclem.github.io/resume">Resume</a>

---

## Final Project 
Build a webscraper that scrapes specific information of your choice from a website of your choice and puts it into a CSV file.
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
---
## Problem
Create a program that takes users full name regardless of how many spaces are in it and create a random username for them using the first letter of their first name, first 4 of their last name and 4 random numbers appended to the end of the username.

```
import random
import string

def numGen():
    # Generates a random integer between 1111 and 9999
    userNumber = random.randint(1111,9999)
    return userNumber


def nameMaker():
    # using string slicing to take the first name from the fullName with :1
    # as well as the last part of the name using 1:
    firstName = str(fullName[:1])
    lastName = str(fullName[-1:])

    # Creating a variable that accepts only the 3rd character in the strVariable firstName
    f_letter = firstName[2:3]
    # making l_name variable = characters between the first 2 and the last 2 which are [' ']
    l_name = lastName[2:-2]

    # Creates a variable that is equal to the number being generated in numGen function
    randomNum = numGen()

    print(f_letter.lower() + l_name.lower() + str(randomNum))



def passGen():
    ascii_letters = string.ascii_letters

    # loops through all of the ascii letters setting all of them = to variable alphabet
    for alphabet in ascii_letters:
        alphabet = ascii_letters

    # Creating a blank list named passwd
    passwd = []
    i = 0
    while i <= 5:
        # Making list passwd to put a random ascii character for every time i adds 1
        passwd.append(random.choice(alphabet))
        i = i + 1

    # New variable password that joins the blank spaces of passwd that looked like ['','','','','','']
    # so that it comes together without brackets/commas/quotations
    password = ''.join(passwd)
    print(password + str(numGen()))

# opening up both text files
f1 = open("usernameslvl1.txt", "r")
f2 = open("usernameslvl2.txt", "r")


file = str(input("What file would you like to open F1 or F2? "))
# Loops through entire text file and prints out all the names
if file == 'F1':
    for line in f1:
        # strips the \n off of the end of the strings and makes it all lowercase
        line = str(line.strip("\n"))

        fullName = line.split(' ')

        print(str(' '.join(fullName)))

        nameMaker()
        passGen()
        print("\n")
else:
    for line in f2:
        # strips the \n off of the end of the strings and makes it all lowercase
        line = str(line.strip("\n"))

        fullName = line.split(' ')

        # Takes the fullName variable forces it into a string and joins the spaces together using ' '.join()
        print(str(' '.join(fullName)))

        nameMaker()
        passGen()
        print("\n")
        
```
