# Facebook_api
data mining from facebook
# -*-coding:utf-8 -*
import pandas as pd
import json
import urllib
import bs4 as bs
import requests
import csv
count = 0
url = 'https://graph.facebook.com/v2.7/search?access_token=EAACEdEose0cBADAiwZCm8D3iPBqp4SwyvIP0mnfz8Bw1pZCH7ZAgbg8kuNSzKedZCaoFan6FnpAY7XfihuAHUFfh2ghtZA1wlm8l1aGBhonTiPCrov6z0zTWi68pPePUKXJfDNtkk8OAcDqKe9ZCjf6Tnq7uT3hiA948dZCsIdSM09dAdjeR1B2hCpK2TTqOUspmk5hBHGZBVQZDZD&pretty=0&q=toronto&type=event&limit=25&after=MjQZD'
while count < 4:
    abc = urllib.urlopen(url)
    abcd =  json.load(abc)
    for item in abcd['data']:

        b = item['place']
        try:
            c = b['location']['city']
        except Exception:
            pass   

        try:
            d = b['location']['street']
        except Exception:
            pass

        try:
            f = b['location']['zip']
        except Exception:
            pass

        try:
            g = item['description']
        except Exception:
            pass

        status = u','.join(map(unicode, [ g.replace(","," ") + ',' + item['name'] + 
                                       ','+item['start_time']+ ','+item['end_time']+ ','+b['name']+' '+d+' '+ c+' '+f ]))
        print status
        a = abcd['paging']['next']
        url = a
    count = count + 1
