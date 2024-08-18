from bs4 import BeautifulSoup
import requests
import pandas as pd

url = "https://web.archive.org/web/20230902185326/https://en.wikipedia.org/wiki/List_of_countries_by_GDP_%28nominal%29"
page = requests.get(url)
soup = BeautifulSoup(page.text,'html')
print(soup)
soup.find_all('table')
soup.title
soup.text
print(soup.title.text)
print(soup.prettify())

tables = soup.find_all("table")
print(tables)
dataframe = []

for i, table in enumerate(tables):
    rows = table.find_all("tr")[1:]  # skip the first row
    data = []
    for row in rows:
        cols = row.find_all("td")
        cols = [col.text.strip() for col in cols]
        data.append(cols)
    df = pd.DataFrame(data)  
    dataframe.append(df)
dataframe[2]
