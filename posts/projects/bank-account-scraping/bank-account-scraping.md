# How I Scraped My Own Bank Transactions With Selenium

![alt text](./pictures/bank-logo.jpg)

Here is the [source code](https://github.com/gmspringer32/personal-budget-tool/tree/main/scraper). I kept all my bank account information private so you won't be able to see it.

### Introduction

My wife and I have used Mint for our financial budget for a while now. She came to me the other day and said that she heard that Mint is no longer going to upkeep their budget app. Whether or not that was true, I thought, "I bet I could make my own budget tool." While I liked Mint, I wanted something more specific and customizable. Unfortunately, my bank did not have an API that I could use. So I decided to use Selenium to login and scrape my own transactions to use for a personal budget tool.

### Data Collection

As mentioned earlier, I decided to use Selenium for my web scraping. It was tedious, to say the least. There was a lot of searching through HTML to find the correct buttons to press, and, of course, I did not want to press the wrong button and mess up something important. But eventually, I was able to go to each of my accounts that I wanted the transactions for, go through all the available transactions, and create a messy dataset. But at least I had something I could work with now!

Here is some code from my scraping proccess. I made a bank scraper class. 

```python
class BankScraper:
    def __init__(self):
        with open("../secure/bankurl.txt") as file:
            self.url = file.read()
        self.driver = None
        self.credit_card_df = pd.DataFrame()
        self.checking_df = pd.DataFrame()
        self.accounts_df = pd.DataFrame()
        with open("../secure/creditcardaccount") as file:
            self.credit_card_account = file.read()
        with open("../secure/bankaccount") as file:
            self.bank_account = file.read()

     def __startDriver__(self):
        self.driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))
        self.driver.get(self.url)

```

The start driver method opens a chrome driver for selenium to interact with. Then I needed to login

```python
    def __insertUsername__(self, username):
        username_bar = self.driver.find_element(By.ID, 'onlineId1')
        time.sleep(.5)
        username_bar.click()
        username_bar.send_keys(username)
        time.sleep(.5)

    def __insertPassword__(self, password):
        password_bar = self.driver.find_element(By.ID, "passcode1")
        time.sleep(.5)
        password_bar.click()
        password_bar.send_keys(password)
        time.sleep(.5)

    def __clickLogin__(self):
        signin_bar = self.driver.find_element(By.ID, 'signIn')
        signin_bar.click()
```

This is an example of how to use selenium to click elements and to insert text into elements. Then I needed to go into my account and get my transactions.

```python
    def __scrapeCreditCardTransactions__(self):
        date_input = self.driver.find_element(By.CLASS_NAME, 'select-bofa')
        date_input_elements = date_input.find_elements(By.TAG_NAME, 'option')
        min_num = min(12, len(date_input_elements))
        for i in range(0, min_num):
            date_input = self.driver.find_element(By.CLASS_NAME, 'select-bofa')
            date_input.find_elements(By.TAG_NAME, 'option')[i].click()
            transactions = self.driver.find_element(By.ID, "transactions")
            table_html = transactions.get_attribute('outerHTML')
            df = pd.read_html(table_html)[0]
            self.credit_card_df = pd.concat([self.credit_card_df, df])
```

I found the table element and used pandas to read it into a dataframe. 

Next, I needed to clean it. First off, the columns were not named how I wanted them to be. So that was the first thing to change. Then I needed to drop any columns I did not need; that only ended up being one of the columns. Then I dropped all the rows with random values in it, such as "There are no transactions to display for the filter you selected. Try changing your selection in the Type filter." To clean the description of the transaction, I used regular expressions to pick out only what I needed to know. Next came dates; I needed to change them to datetime values in Pandas. Then the amount, I needed to change it from a string to a number.

```python
self.checking_df['amount'] = pd.to_numeric(self.checking_df['amount'].str.replace('$', "",regex=False).str.replace(",", '',regex=False)
```

After cleaning the data I had collected, I realized that I wanted to know what category the transaction was in. I couldn't find it to save my life, so I decided to make a [categories](https://github.com/gmspringer32/personal-budget-tool/blob/main/scraper/categories.py) dictionary that I could use to make category columns. That worked surprisingly great.

This is an example of what the data looks like. Note that is is from dummy data created to look like the data I collected so the values will not be the same

| date                | description                              | category            | amount | account     | subcategory         |
| :------------------ | :--------------------------------------- | :------------------ | -----: | :---------- | :------------------ |
| 2023-10-31 00:00:00 | TURO INC.                                | Travel              |  -0.67 | Credit Card | Travel              |
| 2023-10-29 00:00:00 | Check                                    | Rent                |  -5.53 | Credit Card | Rent                |
| 2023-10-28 00:00:00 | UNITED                                   | Airline             |  -16.6 | Credit Card | Airline             |
| 2023-10-27 00:00:00 | CHOICES                                  | Food                | -71.17 | Credit Card | Fast Food           |
| 2023-10-26 00:00:00 | UTAH TRANSIT AUTHORITY                   | Transportation      |  -1.51 | Credit Card | Transportation      |
| 2023-10-25 00:00:00 | STRANGLING BROTHERS CIRC                 | Entertainment       | -49.88 | Credit Card | Entertainment       |
| 2023-10-24 00:00:00 | LAZ PKG                                  | Parking             |  -9.59 | Credit Card | Parking             |
| 2023-10-23 00:00:00 | CMSVENDT B VENDING                       | Food                | -26.62 | Credit Card | Food Snacks         |
| 2023-10-22 00:00:00 | Bank of America Credit Card Bill Payment | Credit Card Payment | -30.45 | Credit Card | Credit Card Payment |
| 2023-10-21 00:00:00 | SQ GETOUT GAMES                          | Entertainment       | -20.91 | Credit Card | Entertainment       |

Now the data was clean and ready to go!

### Ethical Considerations

The only thing that I had to think about with this project is if I was violating any terms of agreement with my bank. I searched through all the papers and did not see any information on using automation to retrieve my own bank information. I just needed to be careful to not put any of my personal information in a public spot.

### Conclusion

The decision to make a personalized solution presented its own challenges, delving into the intricacies of HTML with Selenium to scrape transaction data from my various accounts. The data collection phase resulted in a raw dataset that demanded meticulous cleaning, involving column restructuring, data pruning, and employing regular expressions for refining transaction descriptions, date conversions, and amount formatting. Ethical considerations centered on ensuring compliance with my bank's terms of agreement, prompting careful handling of personal information. This project, underscored by adaptability and resourcefulness, not only overcame constraints but also laid the groundwork for a personalized budgeting tool, aligning with the initial motivation for a more tailored financial management solution. Now onto creating a dahsboard!

[back](../)
