,<img src="https://www.python.org/static/community_logos/python-logo-generic.svg" alt="HomePage"/>

# StockMarketVisualizer
> Visualizing the biggest market cap companies in the Dow Jones index. URL can be altered with provided link
---

### Table of Contents:

- [Description](#description)
- [Code Snippets](#code-snippets)
- [Summary](#summary)
- [Demo](#demo)




---

## Description

This python script will work as a webscrapper for fetching the Dow Jones index companies and plotting by the biggest market cap.

We will create a function to extract the page (title/components) from the passed url. BeautifulSoup will group the content with it's row.find capability. Structure will then be added to the soup to viewed as a plot by importing matplotlib & squairfy.

Once the content is plotted we will add a color scheme to differeciate the market caps by monetary value.



Depencies we will be using

- beautifulsoup
- matplotlib as pyplot & plt/cm
- squairfy
- requests & datetime


---

## Code Snippets

> Importing libraries/depencies & setting up variables
```python
import requests
from bs4 import BeautifulSoup
import matplotlib.pyplot as plt
import matplotlib.pyplot as cm
import squarify

url = 'https://companiesmarketcap.com/dow-jones/largest-companies-by-market-cap/'

response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

rows = soup.findChildren("tr")

symbols = []
market_caps = []
sizes = []
```

> Creating the function to Structure Soup
```python
for row in rows:
    try:
        symbol = row.find("div", {"class": "company-code"}).text
        market_cap = row.findAll('td')[2].text
        market_caps.append(market_cap)
        symbols.append(symbol)
        
        if market_cap.endswith("T"):
            sizes.append(float(market_cap[1:-2]) * 10 ** 12)
        elif market_cap.endswith("B"):
            sizes.append(float(market_cap[1:-2]) * 10 ** 9)
    except AttributeError:
        pass
```

> Adding the labels, colors & plotting on squairfy using matplotlib.plt
```dart
labels = [f"{symbols[i]}\n({market_caps[i]})" for i in range(len(symbols))]
colors = [plt.cm.tab20c(i / float(len(symbols))) for i in range(len(symbols))]

squarify.plot(sizes=sizes, label=labels, bar_kwargs={"linewidth": 0.5, "edgecolor": "#111111"})

plt.show()
```


---

## Summary
Scripting is a powerful tool when used for automating mundane tasks. A webscrapper can be useful when wanting to pull information from a static webpage where html tags will not alter all that much. Providing these attributes to BeautifulSoup will build a collection of content(soup) where one can choose to filter and display/export.

In this example we plot by the biggest monetary values to lowest. Giving depth by adding a color module showing a gradual change.

Scripting is a must have tool in one's asernal. Looking forward to seeing what else I can automate :). 

Useful Documentation:

- [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#)
- [Requests](https://www.w3schools.com/python/module_requests.asp)
- [Matplotlib](https://matplotlib.org/3.5.0/tutorials/introductory/pyplot.html)
- [Squarify](https://www.analyticsvidhya.com/blog/2021/06/build-treemaps-in-python-using-squarify/)
- [Microsoft Scripting](https://docs.microsoft.com/en-us/windows/python/scripting)

---

## Demo
![HomePage Gif](https://github.com/C-Dev66/StockMarketVisualizer/blob/main/screenshots/StockMarketVisualizer.png)


