# 🕸️ Web Scraping Project: BestBuy Stores & AajTak News Headlines

## 📌 Overview

This project demonstrates web scraping using Python. The original goal was to extract **store details** from BestBuy’s New York store page. However, due to the dynamic nature of the site, the data could not be extracted reliably using either `BeautifulSoup` or `Selenium`.

To still demonstrate scraping capability, I pivoted to extracting **news headlines** from [Aaj Tak](https://www.aajtak.in/), a static and scrape-friendly website.

---

## 🔍 Goal

### Attempted:
- Scrape **store name**, **address**, **pincode**, and **timing** from BestBuy.

### Achieved:
- Scraped **top headlines** from Aaj Tak’s homepage.
- Saved the extracted data into a **CSV file**.

---

## ✅ Aaj Tak Headline Scraper

**Website:** [Aaj Tak](https://www.aajtak.in/)

### Data Collected
- News headlines (from homepage).

### Output

```csv
Headline
"India vs Pakistan series may return"
"PM Modi visits Varanasi"
...
```

### Python Script

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

url = "https://www.aajtak.in/"
response = requests.get(url)
soup = BeautifulSoup(response.content, 'html.parser')

headlines = [tag.get_text(strip=True) for tag in soup.find_all('h3') if tag.get_text(strip=True)]

df = pd.DataFrame({'Headline': headlines})
df.to_csv('aajtak_headlines.csv', index=False)
```

---

## ❌ BestBuy Scraper (Unsuccessful)

**Website:** [BestBuy Store Locator (NY)](https://stores.bestbuy.com/ny/new-york.html)

### Issue:
Despite using `Selenium`, the store data didn’t load or was rendered through JavaScript after page load, making it hard to scrape.

### Libraries Used:
- `selenium`
- `webdriver-manager`
- `pandas`

> ❗ Pages rendered via JavaScript are harder to scrape without headless browsers or proper event handling.

---

## 🛠 Installation

Install required packages using:

```bash
pip install requests beautifulsoup4 pandas selenium webdriver-manager
```

---

## 📁 Project Structure

```
📦 WebScrapingProject
 ┣ 📜 aajtak_headlines.csv        # Extracted headlines
 ┣ 📜 bestbuy_scraper.ipynb      # Attempted Selenium script
 ┣ 📜 aajtak_scraper.py          # Working script for Aaj Tak
 ┗ 📜 README.md                  # Project documentation
```

---

## 🧠 Learning Outcome

- JavaScript-rendered sites require special handling (e.g., Selenium with proper waits, proxies, or browser automation).
- Static HTML pages (like Aaj Tak) are easier and faster to scrape.
- Saving scraped data into CSV with `pandas` is simple and useful for analysis.

---

## 🙏 Acknowledgements

- [Aaj Tak - India’s Leading News Website](https://www.aajtak.in/)
- [BestBuy Store Locator](https://stores.bestbuy.com/)
