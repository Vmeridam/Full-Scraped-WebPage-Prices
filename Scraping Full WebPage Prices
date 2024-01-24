import requests
from bs4 import BeautifulSoup
import pandas as pd

url = "https://www.dia.es/compra-online/"

def get_data(url_sample):
    r = requests.get(url_sample)
    soup = BeautifulSoup(r.text,"html.parser")
    return soup

def links(soup):
    link_list = []
    results = soup.find_all("a", {"class":"btn-category"})
    w = "https://www.dia.es/"
    for i in results:
        a = i.get("href")
        link_list.append(w + a)
    href_list = set(link_list)
    print(href_list)
    return href_list

def title_soldprice( results_2):
    r_link = get_data(results_2)
    products_list = []
    results = r_link.find_all("div", {"class": "product-list__item"})
    n = 0
    for item in results:
        products = {
            "title": item.find("span", {"class": "details"}).text,
            "soldprice": item.find("p", {"class": "price"}).text.replace("&nbsp€", "").split()[0],
        }
        products_list.append(products)
    return products_list

soup = get_data(url)
a = links(soup)
t = 0
for i in a:
    try:
        n = 0
        while n == 0:
            productsdf = pd.DataFrame(title_soldprice(i))
            productsdf.to_csv("dia_scrappers999.csv", mode='a', header=False)
            k = get_data(i).find(rel="next").get("href")
            t +=1
            print("hoja numero: ", t)

    except:
        print("han error has occurred")

read_file = pd.read_csv("dia_scrappers999.csv")
read_file.to_excel("dia_scrappers999.xlsx", index=None)
