from autoscraper import AutoScraper
import pandas as pd
import requests
import urllib.request
import requests
import random
from time import sleep
from random import randint


#Mounting google drive in colab to save data
from google.colab import drive
drive.mount('/content/gdrive')

'''Building the autoscraper
item_list=["Give the url of one image in the link"]
amazon_url="url of the website'''


item_list=["https://m.media-amazon.com/images/I/61gqf3Ufn4L._AC_UL320_.jpg"]
amazon_url="https://www.amazon.in/s?i=apparel&bbn=1968542031&rh=n%3A1571271031%2Cn%3A1953602031%2Cn%3A11400137031%2Cn%3A1968542031%2Cn%3A1968543031&dc&fs=true&page=2"

scraper=AutoScraper()
result=scraper.build(amazon_url,item_list)
data = scraper.get_result_similar(amazon_url,grouped=True)
print(data)

#Set the aliases for the rule and save the scraper model.Make sure you copy the rules correctly.
scraper.set_rule_aliases({'rule_rzak':'url'})
scraper.keep_rules(['rule_rzak'])
scraper.save('amazon-search')



#Looping through the url's of the required product and saving to google drive.
search_list = ["apparel"]
image_no = 0

for searchitem in search_list:
      for i in range(1,30):
          search = searchitem
          amazon_url="https://www.amazon.in/s?i={}&bbn=1968253031&rh=n%3A1571271031%2Cn%3A1953602031%2Cn%3A1968253031%2Cn%3A1968257031&dc&fs=true&page={}".format(search,i)
          print(amazon_url)


          data = scraper.get_result_similar(amazon_url,group_by_alias=True)
          print(data)

          for i in data.values():
            for img_link  in i:
                print(img_link)
                image = requests.get(img_link)
                with open('/content/gdrive/MyDrive/Data/EthnicWear/'+searchitem+'/images'+str(image_no),'wb') as f:
                        f.write(image.content)
                        image_no+=1
          sleep(randint(2,10))  
