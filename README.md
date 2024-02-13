```
import requests


response = requests.get("https://api-server.dataquest.io/economic_data/countries?filter_by=region=South Asia")
region_south_asia = response.json()
print(region_south_asia)


```


```
import requests
import json


response=requests.get("https://api-server.dataquest.io/economic_data/indicators?filter_by=topic=Health: Risk factors&filter_by=periodicity=Biennial")
topic_str = response.json()
topic=json.loads(topic_str)
for row in topic:
    print(f"indicator Code: {row['series_code']}")
    print(f"Indicator Name: {row['indicator_name']}")
    break


```

```
import requests

try:
    response = requests.get("https://api-server.dataquest.io/economic_data/indicators?filter_by=indicator_period=Biennial")
    data = response.json()
except Exception as e:
    print("An error occurred with the request:", e)

print(data)
```

```
import requests

parameters = {
    "limit": 5,   
    "offset": 3  
}
response = requests.get("https://api-server.dataquest.io/economic_data/indicators", params=parameters)
data = response.json()
```


```

import requests
import json 


parameters = {
    "limit": 10,  
    "offset": 0  
}
response = requests.get("https://api-server.dataquest.io/economic_data/indicators", params=parameters)
indicator_page_str = response.json()
indicator_page=json.loads(indicator_page_str)
indicator_len_records = len(indicator_page)
fourth_indicator_name =  indicator_page[3].get("indicator_name", [])
print(indicator_len_records)
print(fourth_indicator_name)
```

```
import requests
import json


parameters = {
    "limit": 50,  
    "offset": 0   
}
response = requests.get("https://api-server.dataquest.io/economic_data/indicators", params=parameters)
data_page_1 = json.loads(response.json())
print("Limit (total records):", len(data_page_1))
print("First topic:", data_page_1[0].get("topic", []))
parameters["offset"] = 50
response = requests.get("https://api-server.dataquest.io/economic_data/indicators", params=parameters)
data_page_2 = json.loads(response.json())
print("New topic:",data_page_2[0].get("topic", []))

```

```
import requests
import json


parameters = {
    "filter_by":"currency_unit=Euro,income_group=High income",
    "limit": 5,
    "offset": 0
}


response = requests.get("https://api-server.dataquest.io/economic_data/countries", params=parameters)
data_str = response.json()
data = json.loads(data_str)

for record in data:
    print(record.get("country_code"))
```

```
import requests
import json


parameters = {
    "filter_by":"region=Europe & Central Asia,income_group=Upper middle income",
    "limit": 5,
    "offset": 0
}
response = requests.get("https://api-server.dataquest.io/economic_data/countries", params=parameters)
data_combined_str = response.json()
data_combined=json.loads(data_combined_str)
for record in data_combined:
    country_name=record.get("table_name")
    print(country_name)
```


```
import requests


# Set base URL and endpoint
base_url = "https://api-server.dataquest.io/economic_data"
endpoint = "/historical_data"

# Set query parameters with pagination
parameters = {
    "country_code": "IND",
    "indicator_code": "SP.POP.TOTL",
    "from_year": 2000,
    "to_year": 2020,
    "page": 1,         # Current page number
    "page_number": 50  # Number of records per page
}

# Send GET request
response = requests.get(base_url + endpoint, params=parameters)
data = response.json()

# Print first 5 records
print(data["records"][:5])

# Handling total number of records
total_records = data["total"]
print(f"Total records available: {total_records}")
```
