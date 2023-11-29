---
layout: default
---
[back](../)


* Introduction and motivation for your chosen topic and research question.
* A description of how data was collected and cleaned.
* An explanation of the ethical considerations and measures taken during web scraping.
* A concluding statement.

# How I Scraped My Own Bank Transactions With Selenium

Here is the [source code](https://github.com/gmspringer32/personal-budget-tool/tree/main/scraper). I kept all my bank account information private so you won't be able to see it.

### Introduction

My wife and I have used Mint for our financial budget for a while now. She came to me the other day and said that she heard that Mint is no longer going to upkeep their budget app. Whether or not that was true, I thought, "I bet I could make my own budget tool." While I liked Mint, I wanted something more specific and customizable. Unfortunately, my bank did not have an API that I could use. So I decided to use Selenium to login and scrape my own transactions to use for a personal budget tool.

### Data Collection

As said above, I decided to use selenium for my web scraping. It was teidious to say the least. There was a lot of searching through HTML to find the correct buttons to press, and of course I did not want to press the wrong button and mess up something important. But eventually I was able to go to each of my accounts that I wanted the transactions for, go through all of the available transactions, and create a messy dataset. But at least I have something I can work with now!

Now I needed to clean it. First off, the columns were not named how I wanted them to be. So that was the first thing to change. Then I needed to drop any columns I did not need, that only ended up being one of the columns. Then I dropped all the rows with random values in it such as "There are no transactions to display for the filter you selected. Try changing your selection in the Type filter." Then to clean the description of the transaction, I used regular expressions to pick out only what I needed to know. Next came dates, I needed to change them to datetime values in pandas. Then the amount, I needed to change it from a string to a number. 

After cleaning the data I collected, I realized that I wanted to know what category the transaction is in. I could not find it to save my life, so I decided to make a [categories](https://github.com/gmspringer32/personal-budget-tool/blob/main/scraper/categories.py) dictionary that I could use to make category columns. That worked surprisingly great. 

Now the data was clean and ready to go!
