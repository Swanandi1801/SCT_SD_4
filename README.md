import requests
from bs4 import BeautifulSoup
import csv

url = "http://quotes.toscrape.com/"
headers = {"User-Agent": "Mozilla/5.0"}

response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")

quotes = soup.find_all("div", class_="quote")

with open("quotes.csv", "w", newline="", encoding="utf-8-sig") as file:
    writer = csv.writer(file)
    writer.writerow(["Quote", "Author", "Tags"])

  for q in quotes:
        text = q.find("span", class_="text").text.strip()
        author = q.find("small", class_="author").text.strip()
        tags = ", ".join([tag.text for tag in q.find_all("a", class_="tag")])

  writer.writerow([text, author, tags])

print("Scraping completed successfully!")
