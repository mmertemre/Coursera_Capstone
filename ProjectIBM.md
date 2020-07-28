```python
import requests # library to handle requests
import pandas as pd # library for data analsysis
import numpy as np # library to handle data in a vectorized manner
import random # library for random number generation

!conda install -c conda-forge geopy --yes 
from geopy.geocoders import Nominatim # module to convert an address into latitude and longitude values

# libraries for displaying images
from IPython.display import Image 
from IPython.core.display import HTML 
    
# tranforming json file into a pandas dataframe library
from pandas.io.json import json_normalize

!conda install -c conda-forge folium=0.5.0 --yes
import folium # plotting library

print('Folium installed')
print('Libraries imported.')
```

    Collecting package metadata (current_repodata.json): done
    Solving environment: done
    
    # All requested packages already installed.
    
    Collecting package metadata (current_repodata.json): done
    Solving environment: done
    
    # All requested packages already installed.
    
    Folium installed
    Libraries imported.



```python
CLIENT_ID = '0RHQV0FBMRNOWZVVEAOI5CLSTZY3JJO2P2HFVHDCQVHOH4AM' # your Foursquare ID
CLIENT_SECRET = 'X05TQTCX31WKBYEC3YHMY2AXIF3GVPUOXJXVIRBK5VDYRVK4' # your Foursquare Secret
VERSION = '20180604'
LIMIT = 50
print('Your credentails:')
print('CLIENT_ID: ' + CLIENT_ID)
print('CLIENT_SECRET:' + CLIENT_SECRET)
```

    Your credentails:
    CLIENT_ID: 0RHQV0FBMRNOWZVVEAOI5CLSTZY3JJO2P2HFVHDCQVHOH4AM
    CLIENT_SECRET:X05TQTCX31WKBYEC3YHMY2AXIF3GVPUOXJXVIRBK5VDYRVK4



```python
address = 'Piazza Ventiquattro Maggio, 20123 Milano MI, Italy'

geolocator = Nominatim(user_agent="foursquare_agent")
location = geolocator.geocode(address)
latitude = location.latitude
longitude = location.longitude
print(latitude, longitude)
```

    45.4530314 9.1797111



```python
search_query = 'Food , Cafe'
radius = 1500
print(search_query + ' .... OK!')

```

    Food , Cafe .... OK!



```python
url = 'https://api.foursquare.com/v2/venues/search?client_id={}&client_secret={}&ll={},{}&v={}&query={}&radius={}&limit={}'.format(CLIENT_ID, CLIENT_SECRET, latitude, longitude, VERSION, search_query, radius, LIMIT)
url
```




    'https://api.foursquare.com/v2/venues/search?client_id=0RHQV0FBMRNOWZVVEAOI5CLSTZY3JJO2P2HFVHDCQVHOH4AM&client_secret=X05TQTCX31WKBYEC3YHMY2AXIF3GVPUOXJXVIRBK5VDYRVK4&ll=45.4530314,9.1797111&v=20180604&query=Food , Cafe&radius=1500&limit=50'




```python
results = requests.get(url).json()
results
```




    {'meta': {'code': 200, 'requestId': '5f20341e531fe8660054452e'},
     'response': {'venues': [{'id': '4bc85023af07a5935c95802d',
        'name': 'Noir Cafè',
        'location': {'address': 'Corso di Porta Ticinese, 106',
         'crossStreet': 'Piazza XXIV Maggio',
         'lat': 45.45324304241601,
         'lng': 9.180370242615018,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45324304241601,
           'lng': 9.180370242615018}],
         'distance': 56,
         'postalCode': '20123',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Corso di Porta Ticinese, 106 (Piazza XXIV Maggio)',
          '20123 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d155941735',
          'name': 'Gastropub',
          'pluralName': 'Gastropubs',
          'shortName': 'Gastropub',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/gastropub_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '523186b7498e5dfd5c05a722',
        'name': 'Mont Real cafè',
        'location': {'address': 'P.zza XXIV Maggio, 12',
         'lat': 45.45281839559005,
         'lng': 9.17879600410648,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45281839559005,
           'lng': 9.17879600410648}],
         'distance': 75,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['P.zza XXIV Maggio, 12',
          'Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4fa255c70cd61194eb83c2a2',
        'name': 'Food Land',
        'location': {'address': 'Via Cesare da Sesto 24',
         'lat': 45.45886637945126,
         'lng': 9.171159267425537,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45886637945126,
           'lng': 9.171159267425537}],
         'distance': 931,
         'postalCode': '20123',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Cesare da Sesto 24',
          '20123 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d118951735',
          'name': 'Grocery Store',
          'pluralName': 'Grocery Stores',
          'shortName': 'Grocery Store',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/food_grocery_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4b058879f964a520f7c722e3',
        'name': "Henry's Cafè",
        'location': {'address': 'Via Col di Lana 4',
         'lat': 45.452190737058615,
         'lng': 9.181981918291063,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.452190737058615,
           'lng': 9.181981918291063}],
         'distance': 200,
         'postalCode': '20136',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Col di Lana 4',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d11b941735',
          'name': 'Pub',
          'pluralName': 'Pubs',
          'shortName': 'Pub',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/pub_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4dc98be1d164c28eea865e86',
        'name': 'Mont Real Café',
        'location': {'address': 'Piazza 24 Maggio',
         'lat': 45.45240763943264,
         'lng': 9.178822631514953,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45240763943264,
           'lng': 9.178822631514953}],
         'distance': 98,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Piazza 24 Maggio', 'Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d116941735',
          'name': 'Bar',
          'pluralName': 'Bars',
          'shortName': 'Bar',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/pub_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '52f4a08a11d22d9cc2e6a464',
        'name': 'Food Genius Academy',
        'location': {'address': 'Viale Col Di Lana 8',
         'lat': 45.45094257043446,
         'lng': 9.184125772280348,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45094257043446,
           'lng': 9.184125772280348}],
         'distance': 415,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Viale Col Di Lana 8',
          'Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d171941735',
          'name': 'Event Space',
          'pluralName': 'Event Spaces',
          'shortName': 'Event Space',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/building/eventspace_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4bcdaf56937ca5937017ad92',
        'name': 'Mag Cafè',
        'location': {'address': 'Ripa di Porta Ticinese 43',
         'lat': 45.451301,
         'lng': 9.173428,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.451301,
           'lng': 9.173428}],
         'distance': 527,
         'postalCode': '20143',
         'cc': 'IT',
         'neighborhood': 'Navigli',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Ripa di Porta Ticinese 43',
          '20143 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d11e941735',
          'name': 'Cocktail Bar',
          'pluralName': 'Cocktail Bars',
          'shortName': 'Cocktail',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/cocktails_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4f5aa1c9e4b086681a5e5149',
        'name': 'Sofa Cafe',
        'location': {'address': 'Ripa di Porta Ticinese 7',
         'lat': 45.45203287279338,
         'lng': 9.176716804504393,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45203287279338,
           'lng': 9.176716804504393}],
         'distance': 258,
         'postalCode': '20143',
         'cc': 'IT',
         'neighborhood': 'Navigli',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Ripa di Porta Ticinese 7',
          '20143 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d11e941735',
          'name': 'Cocktail Bar',
          'pluralName': 'Cocktail Bars',
          'shortName': 'Cocktail',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/cocktails_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4f79a788e4b03c36a2c311c2',
        'name': 'Rinascente Food Market',
        'location': {'address': 'Piazza del Duomo',
         'lat': 45.464846428758655,
         'lng': 9.191795655397502,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.464846428758655,
           'lng': 9.191795655397502}],
         'distance': 1618,
         'postalCode': '20121',
         'cc': 'IT',
         'neighborhood': 'Duomo',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Piazza del Duomo',
          '20121 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d1f5941735',
          'name': 'Gourmet Shop',
          'pluralName': 'Gourmet Shops',
          'shortName': 'Gourmet',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/food_gourmet_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4eb5adde4901cef9d8a75f6b',
        'name': 'Prince Cafè',
        'location': {'address': 'Via Giuseppe Lagrange 15',
         'crossStreet': 'Via Cardinale Ascanio Sforza',
         'lat': 45.448767636815425,
         'lng': 9.177261564215286,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.448767636815425,
           'lng': 9.177261564215286}],
         'distance': 511,
         'postalCode': '20136',
         'cc': 'IT',
         'neighborhood': 'Navigli',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Giuseppe Lagrange 15 (Via Cardinale Ascanio Sforza)',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d11e941735',
          'name': 'Cocktail Bar',
          'pluralName': 'Cocktail Bars',
          'shortName': 'Cocktail',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/cocktails_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4c87759147cc224b7121b19f',
        'name': 'Poker Food',
        'location': {'address': 'Via Larga, 1',
         'lat': 45.46228,
         'lng': 9.19438,
         'labeledLatLngs': [{'label': 'display', 'lat': 45.46228, 'lng': 9.19438}],
         'distance': 1540,
         'postalCode': '20122',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Larga, 1', '20122 Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d1c4941735',
          'name': 'Restaurant',
          'pluralName': 'Restaurants',
          'shortName': 'Restaurant',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/default_',
           'suffix': '.png'},
          'primary': True}],
        'venuePage': {'id': '49994476'},
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4c77db03a690236a15909eb5',
        'name': 'Fashion Cafè',
        'location': {'address': 'Corso San Gottardo 51',
         'lat': 45.44685175757527,
         'lng': 9.179397478659045,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.44685175757527,
           'lng': 9.179397478659045}],
         'distance': 688,
         'postalCode': '20136',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Corso San Gottardo 51',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4f326730e4b010a3c12323d6',
        'name': 'Just Café',
        'location': {'address': 'via Francesco Novati, 4',
         'lat': 45.460197915588935,
         'lng': 9.177142379955997,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.460197915588935,
           'lng': 9.177142379955997}],
         'distance': 822,
         'postalCode': '20123',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['via Francesco Novati, 4',
          '20123 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '5281f9df11d2dc6ddc2a68e3',
        'name': 'Food Art',
        'location': {'address': 'Via Vigevano, 34',
         'lat': 45.45,
         'lng': 9.17,
         'labeledLatLngs': [{'label': 'display', 'lat': 45.45, 'lng': 9.17}],
         'distance': 830,
         'postalCode': '20144',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Vigevano, 34',
          '20144 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d1c4941735',
          'name': 'Restaurant',
          'pluralName': 'Restaurants',
          'shortName': 'Restaurant',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/default_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4f0463f5b6348c9d318e4194',
        'name': 'MJM lounge cafe',
        'location': {'address': 'Viale Tibaldi 23',
         'lat': 45.443810193636445,
         'lng': 9.1811405551119,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.443810193636445,
           'lng': 9.1811405551119}],
         'distance': 1032,
         'postalCode': '20143',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Viale Tibaldi 23',
          '20143 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '51658db6e4b04d92cb664989',
        'name': 'Food Experience Mondadori',
        'location': {'address': 'Via TORTONA 15',
         'lat': 45.45293896303574,
         'lng': 9.167421126274123,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45293896303574,
           'lng': 9.167421126274123}],
         'distance': 959,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via TORTONA 15', 'Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d1f1931735',
          'name': 'General Entertainment',
          'pluralName': 'General Entertainment',
          'shortName': 'Entertainment',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/arts_entertainment/default_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4d4c1b321ae4370462bbf060',
        'name': 'Auditorium Cafè',
        'location': {'address': 'Corso San Gottardo, 44',
         'lat': 45.446916542494236,
         'lng': 9.179446460863968,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.446916542494236,
           'lng': 9.179446460863968}],
         'distance': 681,
         'postalCode': '20136',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Corso San Gottardo, 44',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d116941735',
          'name': 'Bar',
          'pluralName': 'Bars',
          'shortName': 'Bar',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/pub_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '5f1343c93e69c67253314097',
        'name': 'Milano Carrabean Food & Drinks',
        'location': {'lat': 45.458923,
         'lng': 9.18262,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.458923,
           'lng': 9.18262}],
         'distance': 694,
         'postalCode': '20123',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['20123 Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d144941735',
          'name': 'Caribbean Restaurant',
          'pluralName': 'Caribbean Restaurants',
          'shortName': 'Caribbean',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/caribbean_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '51655da1e4b06f9467d611d1',
        'name': 'Food&design',
        'location': {'lat': 45.45340468743085,
         'lng': 9.16724366918364,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45340468743085,
           'lng': 9.16724366918364}],
         'distance': 974,
         'cc': 'IT',
         'country': 'Italia',
         'formattedAddress': ['Italia']},
        'categories': [{'id': '4bf58dd8d48988d1f1931735',
          'name': 'General Entertainment',
          'pluralName': 'General Entertainment',
          'shortName': 'Entertainment',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/arts_entertainment/default_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4c11411ed917c9289669b562',
        'name': 'Bordò Cafe',
        'location': {'lat': 45.447631967679506,
         'lng': 9.177105989703792,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.447631967679506,
           'lng': 9.177105989703792}],
         'distance': 634,
         'cc': 'IT',
         'country': 'Italia',
         'formattedAddress': ['Italia']},
        'categories': [{'id': '4bf58dd8d48988d11e941735',
          'name': 'Cocktail Bar',
          'pluralName': 'Cocktail Bars',
          'shortName': 'Cocktail',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/cocktails_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4eb5c4ca02d5f33e92ba3c11',
        'name': "MurPhy's Cafè",
        'location': {'lat': 45.4521877613591,
         'lng': 9.181897270115252,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.4521877613591,
           'lng': 9.181897270115252}],
         'distance': 194,
         'cc': 'IT',
         'country': 'Italia',
         'formattedAddress': ['Italia']},
        'categories': [{'id': '4bf58dd8d48988d116941735',
          'name': 'Bar',
          'pluralName': 'Bars',
          'shortName': 'Bar',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/pub_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '5b4127dfd3cce80039479fe7',
        'name': 'Prima Food and Bar',
        'location': {'lat': 45.451132,
         'lng': 9.171222,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.451132,
           'lng': 9.171222}],
         'distance': 695,
         'postalCode': '20144',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['20144 Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d11e941735',
          'name': 'Cocktail Bar',
          'pluralName': 'Cocktail Bars',
          'shortName': 'Cocktail',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/cocktails_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4ecfb659be7b9eecdf1b2e73',
        'name': 'Time Café',
        'location': {'address': 'Corso di Porta Romana',
         'lat': 45.46042618092384,
         'lng': 9.188427086970098,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.46042618092384,
           'lng': 9.188427086970098}],
         'distance': 1068,
         'postalCode': '20122',
         'cc': 'IT',
         'neighborhood': 'Duomo',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Corso di Porta Romana',
          '20122 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4d20708f5c4ca1cd7146a13d',
        'name': 'Tixy Cafe',
        'location': {'address': 'Corso di porta ticinese, 102',
         'lat': 45.45476068132517,
         'lng': 9.180574801408147,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45476068132517,
           'lng': 9.180574801408147}],
         'distance': 203,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Corso di porta ticinese, 102',
          'Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4e6720b88877dfcf30092d75',
        'name': 'Grunge Cafè',
        'location': {'lat': 45.452108,
         'lng': 9.182572,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.452108,
           'lng': 9.182572}],
         'distance': 245,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '5abe8575ad17896eda57ce05',
        'name': 'DOT - Chianti Street Food',
        'location': {'address': 'Via Orti, 1',
         'lat': 45.45469,
         'lng': 9.19819,
         'labeledLatLngs': [{'label': 'display', 'lat': 45.45469, 'lng': 9.19819}],
         'distance': 1454,
         'postalCode': '20122',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Orti, 1', '20122 Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d147941735',
          'name': 'Diner',
          'pluralName': 'Diners',
          'shortName': 'Diner',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/diner_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '5ef24a389652d200076f0ae9',
        'name': 'Food Benefit',
        'location': {'address': 'Piazza Diaz Armando, 6',
         'lat': 45.4622525,
         'lng': 9.1895074,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.4622525,
           'lng': 9.1895074}],
         'distance': 1280,
         'postalCode': '20123',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Piazza Diaz Armando, 6',
          '20123 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '50aa9e744b90af0d42d5de0e',
          'name': 'Health Food Store',
          'pluralName': 'Health Food Stores',
          'shortName': 'Health Food Store',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/food_grocery_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4bdb58be2a3a0f471d96aeb6',
        'name': 'Martin Cafè',
        'location': {'address': 'Corso di Porta Ticinese',
         'crossStreet': 'Colonne di San Lorenzo',
         'lat': 45.45781904525345,
         'lng': 9.181099562049186,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45781904525345,
           'lng': 9.181099562049186}],
         'distance': 543,
         'postalCode': '20144',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Corso di Porta Ticinese (Colonne di San Lorenzo)',
          '20144 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d11e941735',
          'name': 'Cocktail Bar',
          'pluralName': 'Cocktail Bars',
          'shortName': 'Cocktail',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/cocktails_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '5b2beca462845c002446729e',
        'name': 'Macha Café',
        'location': {'address': 'Viale Col di Lana 5',
         'lat': 45.452236,
         'lng': 9.183117,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.452236,
           'lng': 9.183117}],
         'distance': 280,
         'postalCode': '20136',
         'cc': 'IT',
         'neighborhood': 'Ticinese',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Viale Col di Lana 5',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d111941735',
          'name': 'Japanese Restaurant',
          'pluralName': 'Japanese Restaurants',
          'shortName': 'Japanese',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/japanese_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4c12c220a1010f4737784918',
        'name': 'Antik Cafè',
        'location': {'address': 'Via Ascanio Sforza, 47',
         'crossStreet': 'Via Pavia',
         'lat': 45.447443339206096,
         'lng': 9.177283559538386,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.447443339206096,
           'lng': 9.177283559538386}],
         'distance': 650,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Ascanio Sforza, 47 (Via Pavia)',
          'Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d116941735',
          'name': 'Bar',
          'pluralName': 'Bars',
          'shortName': 'Bar',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/pub_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4c8b620ca92fa093a2139abf',
        'name': 'Gran Cafè Visconteo',
        'location': {'address': 'Piazza Duomo 17',
         'lat': 45.464081473476206,
         'lng': 9.18855882369763,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.464081473476206,
           'lng': 9.18855882369763}],
         'distance': 1410,
         'postalCode': '20123',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Piazza Duomo 17',
          '20123 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d110941735',
          'name': 'Italian Restaurant',
          'pluralName': 'Italian Restaurants',
          'shortName': 'Italian',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/italian_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4ee60ae693adf8e1a91a3d76',
        'name': 'JJ Cafe',
        'location': {'address': 'Viale Col Di Lana',
         'lat': 45.45221230652198,
         'lng': 9.182938383154724,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45221230652198,
           'lng': 9.182938383154724}],
         'distance': 268,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Viale Col Di Lana', 'Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '5b9c095f82a750002cd4d90e',
        'name': 'Thoka Cafè',
        'location': {'lat': 45.450727,
         'lng': 9.180099,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.450727,
           'lng': 9.180099}],
         'distance': 258,
         'postalCode': '20136',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['20136 Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4da8da3e0cb6a89c624857c6',
        'name': "Glice cafe'",
        'location': {'lat': 45.451342893184645,
         'lng': 9.177687016929918,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.451342893184645,
           'lng': 9.177687016929918}],
         'distance': 245,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4cc08a8b00d8370407454b5c',
        'name': 'Pizza And Food',
        'location': {'address': 'Via Gorizia',
         'lat': 45.45435883001174,
         'lng': 9.173813803413882,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45435883001174,
           'lng': 9.173813803413882}],
         'distance': 483,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Gorizia', 'Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d1ca941735',
          'name': 'Pizza Place',
          'pluralName': 'Pizza Places',
          'shortName': 'Pizza',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/pizza_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '50b4c817e4b03acff52c607d',
        'name': 'Cafè Liberty',
        'location': {'address': 'Corso Di Porta Vigentina',
         'lat': 45.4539358858302,
         'lng': 9.196072784628903,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.4539358858302,
           'lng': 9.196072784628903}],
         'distance': 1281,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Corso Di Porta Vigentina',
          'Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '50b0bacbe4b012a766a98a19',
        'name': "Design Cafe' Gourmet",
        'location': {'address': 'Via Savona 11',
         'lat': 45.455436206536085,
         'lng': 9.168307524060685,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.455436206536085,
           'lng': 9.168307524060685}],
         'distance': 929,
         'postalCode': '20143',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Savona 11',
          '20143 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d110941735',
          'name': 'Italian Restaurant',
          'pluralName': 'Italian Restaurants',
          'shortName': 'Italian',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/italian_',
           'suffix': '.png'},
          'primary': True}],
        'venuePage': {'id': '46187699'},
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4c74d49644d395214e59f7be',
        'name': 'Pierre Cafè',
        'location': {'address': 'Via Broletto, 18',
         'lat': 45.46690475054616,
         'lng': 9.185934215690914,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.46690475054616,
           'lng': 9.185934215690914}],
         'distance': 1619,
         'postalCode': '20121',
         'cc': 'IT',
         'neighborhood': 'Centro Storico',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Broletto, 18',
          '20121 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4c7fa0792042b1f75958c3ad',
        'name': 'Dada Cafè',
        'location': {'address': 'Superstudio Più',
         'crossStreet': 'via Tortona 27',
         'lat': 45.45045119254735,
         'lng': 9.163570197139657,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45045119254735,
           'lng': 9.163570197139657}],
         'distance': 1292,
         'postalCode': '20144',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Superstudio Più (via Tortona 27)',
          '20144 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4e5293c518a86770c586725c',
        'name': 'Lucky cafè',
        'location': {'address': 'viale col di lana 14',
         'lat': 45.451931977252485,
         'lng': 9.18425096860439,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.451931977252485,
           'lng': 9.18425096860439}],
         'distance': 375,
         'postalCode': '20136',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['viale col di lana 14',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4bddc5ccffdec928e25be6a1',
        'name': 'Pizza and Food',
        'location': {'address': 'Via Gorizia',
         'lat': 45.454225717448864,
         'lng': 9.174000062729746,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.454225717448864,
           'lng': 9.174000062729746}],
         'distance': 465,
         'postalCode': '20144',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Gorizia', '20144 Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d1ca941735',
          'name': 'Pizza Place',
          'pluralName': 'Pizza Places',
          'shortName': 'Pizza',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/pizza_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4cbf684f985aa35d3fcc4612',
        'name': "Roxanne Cafe'",
        'location': {'address': 'Via Scoglio di Quarto 2',
         'crossStreet': 'Via Ascanio Sforza',
         'lat': 45.45175162393462,
         'lng': 9.178180655196558,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45175162393462,
           'lng': 9.178180655196558}],
         'distance': 185,
         'postalCode': '20136',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Scoglio di Quarto 2 (Via Ascanio Sforza)',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d11a941735',
          'name': 'Other Nightlife',
          'pluralName': 'Other Nightlife',
          'shortName': 'Nightlife',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/default_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4e61870eb0fb188e8d5022c9',
        'name': 'Cafè Clubino',
        'location': {'address': 'Via Cosseria 1',
         'crossStreet': 'Viale Gian Galeazzo',
         'lat': 45.452463437231096,
         'lng': 9.184747235199715,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.452463437231096,
           'lng': 9.184747235199715}],
         'distance': 398,
         'postalCode': '20136',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Cosseria 1 (Viale Gian Galeazzo)',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4e2ff52ac65b80dfd845924c',
        'name': 'Migjorn Cafe',
        'location': {'lat': 45.45567647820877,
         'lng': 9.183897872660575,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45567647820877,
           'lng': 9.183897872660575}],
         'distance': 439,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4ca3457af832a1cd0cfc9be5',
        'name': 'La Galleria Café Bistrot',
        'location': {'address': 'Piazza Duomo',
         'lat': 45.464535418947975,
         'lng': 9.190352259038521,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.464535418947975,
           'lng': 9.190352259038521}],
         'distance': 1526,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Piazza Duomo', 'Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d110941735',
          'name': 'Italian Restaurant',
          'pluralName': 'Italian Restaurants',
          'shortName': 'Italian',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/italian_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4ea546ad490102dac3c6f318',
        'name': 'Good Food',
        'location': {'address': 'Viale Bligny 3',
         'lat': 45.45185278322053,
         'lng': 9.187790595742335,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.45185278322053,
           'lng': 9.187790595742335}],
         'distance': 644,
         'postalCode': '20136',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Viale Bligny 3',
          '20136 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d123941735',
          'name': 'Wine Bar',
          'pluralName': 'Wine Bars',
          'shortName': 'Wine Bar',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/winery_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4f5b9d25e4b06784f7be1bf8',
        'name': 'Soul Food',
        'location': {'address': 'Via Gola 3',
         'lat': 45.44901511031179,
         'lng': 9.176673491296341,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.44901511031179,
           'lng': 9.176673491296341}],
         'distance': 506,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Gola 3', 'Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d1f9941735',
          'name': 'Food & Drink Shop',
          'pluralName': 'Food & Drink Shops',
          'shortName': 'Food & Drink',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/foodanddrink_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4c2a5f4ec758e21e99883a3f',
        'name': 'Free Art Cafè',
        'location': {'address': 'Vigevano, 9',
         'lat': 45.453114,
         'lng': 9.174698,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.453114,
           'lng': 9.174698}],
         'distance': 391,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Vigevano, 9', 'Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d116941735',
          'name': 'Bar',
          'pluralName': 'Bars',
          'shortName': 'Bar',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/pub_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4e05d52e45ddb2875c400801',
        'name': 'Volutta Café',
        'location': {'lat': 45.463031764606754,
         'lng': 9.188423495206859,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.463031764606754,
           'lng': 9.188423495206859}],
         'distance': 1304,
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Milano Lombardia', 'Italia']},
        'categories': [{'id': '4bf58dd8d48988d16d941735',
          'name': 'Café',
          'pluralName': 'Cafés',
          'shortName': 'Café',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False},
       {'id': '4bd03897caff9521825fcef0',
        'name': 'Jade Cafè',
        'location': {'address': 'Via Palazzo Reale 5',
         'lat': 45.462478990467346,
         'lng': 9.192617310011888,
         'labeledLatLngs': [{'label': 'display',
           'lat': 45.462478990467346,
           'lng': 9.192617310011888}],
         'distance': 1456,
         'postalCode': '20122',
         'cc': 'IT',
         'city': 'Milano',
         'state': 'Lombardia',
         'country': 'Italia',
         'formattedAddress': ['Via Palazzo Reale 5',
          '20122 Milano Lombardia',
          'Italia']},
        'categories': [{'id': '4bf58dd8d48988d142941735',
          'name': 'Asian Restaurant',
          'pluralName': 'Asian Restaurants',
          'shortName': 'Asian',
          'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/asian_',
           'suffix': '.png'},
          'primary': True}],
        'referralId': 'v-1595946192',
        'hasPerk': False}]}}




```python
# assign relevant part of JSON to venues
venues = results['response']['venues']

# tranform venues into a dataframe
dataframe = json_normalize(venues)
dataframe.head()
```

    /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages/ipykernel_launcher.py:5: FutureWarning: pandas.io.json.json_normalize is deprecated, use pandas.json_normalize instead
      """





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>categories</th>
      <th>referralId</th>
      <th>hasPerk</th>
      <th>location.address</th>
      <th>location.crossStreet</th>
      <th>location.lat</th>
      <th>location.lng</th>
      <th>location.labeledLatLngs</th>
      <th>location.distance</th>
      <th>location.postalCode</th>
      <th>location.cc</th>
      <th>location.city</th>
      <th>location.state</th>
      <th>location.country</th>
      <th>location.formattedAddress</th>
      <th>location.neighborhood</th>
      <th>venuePage.id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4bc85023af07a5935c95802d</td>
      <td>Noir Cafè</td>
      <td>[{'id': '4bf58dd8d48988d155941735', 'name': 'G...</td>
      <td>v-1595946192</td>
      <td>False</td>
      <td>Corso di Porta Ticinese, 106</td>
      <td>Piazza XXIV Maggio</td>
      <td>45.453243</td>
      <td>9.180370</td>
      <td>[{'label': 'display', 'lat': 45.45324304241601...</td>
      <td>56</td>
      <td>20123</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Corso di Porta Ticinese, 106 (Piazza XXIV Mag...</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>523186b7498e5dfd5c05a722</td>
      <td>Mont Real cafè</td>
      <td>[{'id': '4bf58dd8d48988d16d941735', 'name': 'C...</td>
      <td>v-1595946192</td>
      <td>False</td>
      <td>P.zza XXIV Maggio, 12</td>
      <td>NaN</td>
      <td>45.452818</td>
      <td>9.178796</td>
      <td>[{'label': 'display', 'lat': 45.45281839559005...</td>
      <td>75</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[P.zza XXIV Maggio, 12, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4fa255c70cd61194eb83c2a2</td>
      <td>Food Land</td>
      <td>[{'id': '4bf58dd8d48988d118951735', 'name': 'G...</td>
      <td>v-1595946192</td>
      <td>False</td>
      <td>Via Cesare da Sesto 24</td>
      <td>NaN</td>
      <td>45.458866</td>
      <td>9.171159</td>
      <td>[{'label': 'display', 'lat': 45.45886637945126...</td>
      <td>931</td>
      <td>20123</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Cesare da Sesto 24, 20123 Milano Lombardi...</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4b058879f964a520f7c722e3</td>
      <td>Henry's Cafè</td>
      <td>[{'id': '4bf58dd8d48988d11b941735', 'name': 'P...</td>
      <td>v-1595946192</td>
      <td>False</td>
      <td>Via Col di Lana 4</td>
      <td>NaN</td>
      <td>45.452191</td>
      <td>9.181982</td>
      <td>[{'label': 'display', 'lat': 45.45219073705861...</td>
      <td>200</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Col di Lana 4, 20136 Milano Lombardia, It...</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4dc98be1d164c28eea865e86</td>
      <td>Mont Real Café</td>
      <td>[{'id': '4bf58dd8d48988d116941735', 'name': 'B...</td>
      <td>v-1595946192</td>
      <td>False</td>
      <td>Piazza 24 Maggio</td>
      <td>NaN</td>
      <td>45.452408</td>
      <td>9.178823</td>
      <td>[{'label': 'display', 'lat': 45.45240763943264...</td>
      <td>98</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Piazza 24 Maggio, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# keep only columns that include venue name, and anything that is associated with location
filtered_columns = ['name', 'categories'] + [col for col in dataframe.columns if col.startswith('location.')] + ['id']
dataframe_filtered = dataframe.loc[:, filtered_columns]

# function that extracts the category of the venue
def get_category_type(row):
    try:
        categories_list = row['categories']
    except:
        categories_list = row['venue.categories']
        
    if len(categories_list) == 0:
        return None
    else:
        return categories_list[0]['name']

# filter the category for each row
dataframe_filtered['categories'] = dataframe_filtered.apply(get_category_type, axis=1)

# clean column names by keeping only last term
dataframe_filtered.columns = [column.split('.')[-1] for column in dataframe_filtered.columns]

dataframe_filtered
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>categories</th>
      <th>address</th>
      <th>crossStreet</th>
      <th>lat</th>
      <th>lng</th>
      <th>labeledLatLngs</th>
      <th>distance</th>
      <th>postalCode</th>
      <th>cc</th>
      <th>city</th>
      <th>state</th>
      <th>country</th>
      <th>formattedAddress</th>
      <th>neighborhood</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Noir Cafè</td>
      <td>Gastropub</td>
      <td>Corso di Porta Ticinese, 106</td>
      <td>Piazza XXIV Maggio</td>
      <td>45.453243</td>
      <td>9.180370</td>
      <td>[{'label': 'display', 'lat': 45.45324304241601...</td>
      <td>56</td>
      <td>20123</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Corso di Porta Ticinese, 106 (Piazza XXIV Mag...</td>
      <td>NaN</td>
      <td>4bc85023af07a5935c95802d</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mont Real cafè</td>
      <td>Café</td>
      <td>P.zza XXIV Maggio, 12</td>
      <td>NaN</td>
      <td>45.452818</td>
      <td>9.178796</td>
      <td>[{'label': 'display', 'lat': 45.45281839559005...</td>
      <td>75</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[P.zza XXIV Maggio, 12, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>523186b7498e5dfd5c05a722</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Food Land</td>
      <td>Grocery Store</td>
      <td>Via Cesare da Sesto 24</td>
      <td>NaN</td>
      <td>45.458866</td>
      <td>9.171159</td>
      <td>[{'label': 'display', 'lat': 45.45886637945126...</td>
      <td>931</td>
      <td>20123</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Cesare da Sesto 24, 20123 Milano Lombardi...</td>
      <td>NaN</td>
      <td>4fa255c70cd61194eb83c2a2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Henry's Cafè</td>
      <td>Pub</td>
      <td>Via Col di Lana 4</td>
      <td>NaN</td>
      <td>45.452191</td>
      <td>9.181982</td>
      <td>[{'label': 'display', 'lat': 45.45219073705861...</td>
      <td>200</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Col di Lana 4, 20136 Milano Lombardia, It...</td>
      <td>NaN</td>
      <td>4b058879f964a520f7c722e3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mont Real Café</td>
      <td>Bar</td>
      <td>Piazza 24 Maggio</td>
      <td>NaN</td>
      <td>45.452408</td>
      <td>9.178823</td>
      <td>[{'label': 'display', 'lat': 45.45240763943264...</td>
      <td>98</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Piazza 24 Maggio, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4dc98be1d164c28eea865e86</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Food Genius Academy</td>
      <td>Event Space</td>
      <td>Viale Col Di Lana 8</td>
      <td>NaN</td>
      <td>45.450943</td>
      <td>9.184126</td>
      <td>[{'label': 'display', 'lat': 45.45094257043446...</td>
      <td>415</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Viale Col Di Lana 8, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>52f4a08a11d22d9cc2e6a464</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Mag Cafè</td>
      <td>Cocktail Bar</td>
      <td>Ripa di Porta Ticinese 43</td>
      <td>NaN</td>
      <td>45.451301</td>
      <td>9.173428</td>
      <td>[{'label': 'display', 'lat': 45.451301, 'lng':...</td>
      <td>527</td>
      <td>20143</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Ripa di Porta Ticinese 43, 20143 Milano Lomba...</td>
      <td>Navigli</td>
      <td>4bcdaf56937ca5937017ad92</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Sofa Cafe</td>
      <td>Cocktail Bar</td>
      <td>Ripa di Porta Ticinese 7</td>
      <td>NaN</td>
      <td>45.452033</td>
      <td>9.176717</td>
      <td>[{'label': 'display', 'lat': 45.45203287279338...</td>
      <td>258</td>
      <td>20143</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Ripa di Porta Ticinese 7, 20143 Milano Lombar...</td>
      <td>Navigli</td>
      <td>4f5aa1c9e4b086681a5e5149</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Rinascente Food Market</td>
      <td>Gourmet Shop</td>
      <td>Piazza del Duomo</td>
      <td>NaN</td>
      <td>45.464846</td>
      <td>9.191796</td>
      <td>[{'label': 'display', 'lat': 45.46484642875865...</td>
      <td>1618</td>
      <td>20121</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Piazza del Duomo, 20121 Milano Lombardia, Ita...</td>
      <td>Duomo</td>
      <td>4f79a788e4b03c36a2c311c2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Prince Cafè</td>
      <td>Cocktail Bar</td>
      <td>Via Giuseppe Lagrange 15</td>
      <td>Via Cardinale Ascanio Sforza</td>
      <td>45.448768</td>
      <td>9.177262</td>
      <td>[{'label': 'display', 'lat': 45.44876763681542...</td>
      <td>511</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Giuseppe Lagrange 15 (Via Cardinale Ascan...</td>
      <td>Navigli</td>
      <td>4eb5adde4901cef9d8a75f6b</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Poker Food</td>
      <td>Restaurant</td>
      <td>Via Larga, 1</td>
      <td>NaN</td>
      <td>45.462280</td>
      <td>9.194380</td>
      <td>[{'label': 'display', 'lat': 45.46228, 'lng': ...</td>
      <td>1540</td>
      <td>20122</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Larga, 1, 20122 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4c87759147cc224b7121b19f</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Fashion Cafè</td>
      <td>Café</td>
      <td>Corso San Gottardo 51</td>
      <td>NaN</td>
      <td>45.446852</td>
      <td>9.179397</td>
      <td>[{'label': 'display', 'lat': 45.44685175757527...</td>
      <td>688</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Corso San Gottardo 51, 20136 Milano Lombardia...</td>
      <td>NaN</td>
      <td>4c77db03a690236a15909eb5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Just Café</td>
      <td>Café</td>
      <td>via Francesco Novati, 4</td>
      <td>NaN</td>
      <td>45.460198</td>
      <td>9.177142</td>
      <td>[{'label': 'display', 'lat': 45.46019791558893...</td>
      <td>822</td>
      <td>20123</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[via Francesco Novati, 4, 20123 Milano Lombard...</td>
      <td>NaN</td>
      <td>4f326730e4b010a3c12323d6</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Food Art</td>
      <td>Restaurant</td>
      <td>Via Vigevano, 34</td>
      <td>NaN</td>
      <td>45.450000</td>
      <td>9.170000</td>
      <td>[{'label': 'display', 'lat': 45.45, 'lng': 9.17}]</td>
      <td>830</td>
      <td>20144</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Vigevano, 34, 20144 Milano Lombardia, Ita...</td>
      <td>NaN</td>
      <td>5281f9df11d2dc6ddc2a68e3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>MJM lounge cafe</td>
      <td>Café</td>
      <td>Viale Tibaldi 23</td>
      <td>NaN</td>
      <td>45.443810</td>
      <td>9.181141</td>
      <td>[{'label': 'display', 'lat': 45.44381019363644...</td>
      <td>1032</td>
      <td>20143</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Viale Tibaldi 23, 20143 Milano Lombardia, Ita...</td>
      <td>NaN</td>
      <td>4f0463f5b6348c9d318e4194</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Food Experience Mondadori</td>
      <td>General Entertainment</td>
      <td>Via TORTONA 15</td>
      <td>NaN</td>
      <td>45.452939</td>
      <td>9.167421</td>
      <td>[{'label': 'display', 'lat': 45.45293896303574...</td>
      <td>959</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via TORTONA 15, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>51658db6e4b04d92cb664989</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Auditorium Cafè</td>
      <td>Bar</td>
      <td>Corso San Gottardo, 44</td>
      <td>NaN</td>
      <td>45.446917</td>
      <td>9.179446</td>
      <td>[{'label': 'display', 'lat': 45.44691654249423...</td>
      <td>681</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Corso San Gottardo, 44, 20136 Milano Lombardi...</td>
      <td>NaN</td>
      <td>4d4c1b321ae4370462bbf060</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Milano Carrabean Food &amp; Drinks</td>
      <td>Caribbean Restaurant</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.458923</td>
      <td>9.182620</td>
      <td>[{'label': 'display', 'lat': 45.458923, 'lng':...</td>
      <td>694</td>
      <td>20123</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[20123 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>5f1343c93e69c67253314097</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Food&amp;design</td>
      <td>General Entertainment</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.453405</td>
      <td>9.167244</td>
      <td>[{'label': 'display', 'lat': 45.45340468743085...</td>
      <td>974</td>
      <td>NaN</td>
      <td>IT</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Italia</td>
      <td>[Italia]</td>
      <td>NaN</td>
      <td>51655da1e4b06f9467d611d1</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Bordò Cafe</td>
      <td>Cocktail Bar</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.447632</td>
      <td>9.177106</td>
      <td>[{'label': 'display', 'lat': 45.44763196767950...</td>
      <td>634</td>
      <td>NaN</td>
      <td>IT</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Italia</td>
      <td>[Italia]</td>
      <td>NaN</td>
      <td>4c11411ed917c9289669b562</td>
    </tr>
    <tr>
      <th>20</th>
      <td>MurPhy's Cafè</td>
      <td>Bar</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.452188</td>
      <td>9.181897</td>
      <td>[{'label': 'display', 'lat': 45.4521877613591,...</td>
      <td>194</td>
      <td>NaN</td>
      <td>IT</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Italia</td>
      <td>[Italia]</td>
      <td>NaN</td>
      <td>4eb5c4ca02d5f33e92ba3c11</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Prima Food and Bar</td>
      <td>Cocktail Bar</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.451132</td>
      <td>9.171222</td>
      <td>[{'label': 'display', 'lat': 45.451132, 'lng':...</td>
      <td>695</td>
      <td>20144</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[20144 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>5b4127dfd3cce80039479fe7</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Time Café</td>
      <td>Café</td>
      <td>Corso di Porta Romana</td>
      <td>NaN</td>
      <td>45.460426</td>
      <td>9.188427</td>
      <td>[{'label': 'display', 'lat': 45.46042618092384...</td>
      <td>1068</td>
      <td>20122</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Corso di Porta Romana, 20122 Milano Lombardia...</td>
      <td>Duomo</td>
      <td>4ecfb659be7b9eecdf1b2e73</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Tixy Cafe</td>
      <td>Café</td>
      <td>Corso di porta ticinese, 102</td>
      <td>NaN</td>
      <td>45.454761</td>
      <td>9.180575</td>
      <td>[{'label': 'display', 'lat': 45.45476068132517...</td>
      <td>203</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Corso di porta ticinese, 102, Milano Lombardi...</td>
      <td>NaN</td>
      <td>4d20708f5c4ca1cd7146a13d</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Grunge Cafè</td>
      <td>Café</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.452108</td>
      <td>9.182572</td>
      <td>[{'label': 'display', 'lat': 45.452108, 'lng':...</td>
      <td>245</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4e6720b88877dfcf30092d75</td>
    </tr>
    <tr>
      <th>25</th>
      <td>DOT - Chianti Street Food</td>
      <td>Diner</td>
      <td>Via Orti, 1</td>
      <td>NaN</td>
      <td>45.454690</td>
      <td>9.198190</td>
      <td>[{'label': 'display', 'lat': 45.45469, 'lng': ...</td>
      <td>1454</td>
      <td>20122</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Orti, 1, 20122 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>5abe8575ad17896eda57ce05</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Food Benefit</td>
      <td>Health Food Store</td>
      <td>Piazza Diaz Armando, 6</td>
      <td>NaN</td>
      <td>45.462252</td>
      <td>9.189507</td>
      <td>[{'label': 'display', 'lat': 45.4622525, 'lng'...</td>
      <td>1280</td>
      <td>20123</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Piazza Diaz Armando, 6, 20123 Milano Lombardi...</td>
      <td>NaN</td>
      <td>5ef24a389652d200076f0ae9</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Martin Cafè</td>
      <td>Cocktail Bar</td>
      <td>Corso di Porta Ticinese</td>
      <td>Colonne di San Lorenzo</td>
      <td>45.457819</td>
      <td>9.181100</td>
      <td>[{'label': 'display', 'lat': 45.45781904525345...</td>
      <td>543</td>
      <td>20144</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Corso di Porta Ticinese (Colonne di San Loren...</td>
      <td>NaN</td>
      <td>4bdb58be2a3a0f471d96aeb6</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Macha Café</td>
      <td>Japanese Restaurant</td>
      <td>Viale Col di Lana 5</td>
      <td>NaN</td>
      <td>45.452236</td>
      <td>9.183117</td>
      <td>[{'label': 'display', 'lat': 45.452236, 'lng':...</td>
      <td>280</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Viale Col di Lana 5, 20136 Milano Lombardia, ...</td>
      <td>Ticinese</td>
      <td>5b2beca462845c002446729e</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Antik Cafè</td>
      <td>Bar</td>
      <td>Via Ascanio Sforza, 47</td>
      <td>Via Pavia</td>
      <td>45.447443</td>
      <td>9.177284</td>
      <td>[{'label': 'display', 'lat': 45.44744333920609...</td>
      <td>650</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Ascanio Sforza, 47 (Via Pavia), Milano Lo...</td>
      <td>NaN</td>
      <td>4c12c220a1010f4737784918</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Gran Cafè Visconteo</td>
      <td>Italian Restaurant</td>
      <td>Piazza Duomo 17</td>
      <td>NaN</td>
      <td>45.464081</td>
      <td>9.188559</td>
      <td>[{'label': 'display', 'lat': 45.46408147347620...</td>
      <td>1410</td>
      <td>20123</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Piazza Duomo 17, 20123 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4c8b620ca92fa093a2139abf</td>
    </tr>
    <tr>
      <th>31</th>
      <td>JJ Cafe</td>
      <td>Café</td>
      <td>Viale Col Di Lana</td>
      <td>NaN</td>
      <td>45.452212</td>
      <td>9.182938</td>
      <td>[{'label': 'display', 'lat': 45.45221230652198...</td>
      <td>268</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Viale Col Di Lana, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4ee60ae693adf8e1a91a3d76</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Thoka Cafè</td>
      <td>Café</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.450727</td>
      <td>9.180099</td>
      <td>[{'label': 'display', 'lat': 45.450727, 'lng':...</td>
      <td>258</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[20136 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>5b9c095f82a750002cd4d90e</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Glice cafe'</td>
      <td>Café</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.451343</td>
      <td>9.177687</td>
      <td>[{'label': 'display', 'lat': 45.45134289318464...</td>
      <td>245</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4da8da3e0cb6a89c624857c6</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Pizza And Food</td>
      <td>Pizza Place</td>
      <td>Via Gorizia</td>
      <td>NaN</td>
      <td>45.454359</td>
      <td>9.173814</td>
      <td>[{'label': 'display', 'lat': 45.45435883001174...</td>
      <td>483</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Gorizia, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4cc08a8b00d8370407454b5c</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Cafè Liberty</td>
      <td>Café</td>
      <td>Corso Di Porta Vigentina</td>
      <td>NaN</td>
      <td>45.453936</td>
      <td>9.196073</td>
      <td>[{'label': 'display', 'lat': 45.4539358858302,...</td>
      <td>1281</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Corso Di Porta Vigentina, Milano Lombardia, I...</td>
      <td>NaN</td>
      <td>50b4c817e4b03acff52c607d</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Design Cafe' Gourmet</td>
      <td>Italian Restaurant</td>
      <td>Via Savona 11</td>
      <td>NaN</td>
      <td>45.455436</td>
      <td>9.168308</td>
      <td>[{'label': 'display', 'lat': 45.45543620653608...</td>
      <td>929</td>
      <td>20143</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Savona 11, 20143 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>50b0bacbe4b012a766a98a19</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Pierre Cafè</td>
      <td>Café</td>
      <td>Via Broletto, 18</td>
      <td>NaN</td>
      <td>45.466905</td>
      <td>9.185934</td>
      <td>[{'label': 'display', 'lat': 45.46690475054616...</td>
      <td>1619</td>
      <td>20121</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Broletto, 18, 20121 Milano Lombardia, Ita...</td>
      <td>Centro Storico</td>
      <td>4c74d49644d395214e59f7be</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Dada Cafè</td>
      <td>Café</td>
      <td>Superstudio Più</td>
      <td>via Tortona 27</td>
      <td>45.450451</td>
      <td>9.163570</td>
      <td>[{'label': 'display', 'lat': 45.45045119254735...</td>
      <td>1292</td>
      <td>20144</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Superstudio Più (via Tortona 27), 20144 Milan...</td>
      <td>NaN</td>
      <td>4c7fa0792042b1f75958c3ad</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Lucky cafè</td>
      <td>Café</td>
      <td>viale col di lana 14</td>
      <td>NaN</td>
      <td>45.451932</td>
      <td>9.184251</td>
      <td>[{'label': 'display', 'lat': 45.45193197725248...</td>
      <td>375</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[viale col di lana 14, 20136 Milano Lombardia,...</td>
      <td>NaN</td>
      <td>4e5293c518a86770c586725c</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Pizza and Food</td>
      <td>Pizza Place</td>
      <td>Via Gorizia</td>
      <td>NaN</td>
      <td>45.454226</td>
      <td>9.174000</td>
      <td>[{'label': 'display', 'lat': 45.45422571744886...</td>
      <td>465</td>
      <td>20144</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Gorizia, 20144 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4bddc5ccffdec928e25be6a1</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Roxanne Cafe'</td>
      <td>Other Nightlife</td>
      <td>Via Scoglio di Quarto 2</td>
      <td>Via Ascanio Sforza</td>
      <td>45.451752</td>
      <td>9.178181</td>
      <td>[{'label': 'display', 'lat': 45.45175162393462...</td>
      <td>185</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Scoglio di Quarto 2 (Via Ascanio Sforza),...</td>
      <td>NaN</td>
      <td>4cbf684f985aa35d3fcc4612</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Cafè Clubino</td>
      <td>Café</td>
      <td>Via Cosseria 1</td>
      <td>Viale Gian Galeazzo</td>
      <td>45.452463</td>
      <td>9.184747</td>
      <td>[{'label': 'display', 'lat': 45.45246343723109...</td>
      <td>398</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Cosseria 1 (Viale Gian Galeazzo), 20136 M...</td>
      <td>NaN</td>
      <td>4e61870eb0fb188e8d5022c9</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Migjorn Cafe</td>
      <td>Café</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.455676</td>
      <td>9.183898</td>
      <td>[{'label': 'display', 'lat': 45.45567647820877...</td>
      <td>439</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4e2ff52ac65b80dfd845924c</td>
    </tr>
    <tr>
      <th>44</th>
      <td>La Galleria Café Bistrot</td>
      <td>Italian Restaurant</td>
      <td>Piazza Duomo</td>
      <td>NaN</td>
      <td>45.464535</td>
      <td>9.190352</td>
      <td>[{'label': 'display', 'lat': 45.46453541894797...</td>
      <td>1526</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Piazza Duomo, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4ca3457af832a1cd0cfc9be5</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Good Food</td>
      <td>Wine Bar</td>
      <td>Viale Bligny 3</td>
      <td>NaN</td>
      <td>45.451853</td>
      <td>9.187791</td>
      <td>[{'label': 'display', 'lat': 45.45185278322053...</td>
      <td>644</td>
      <td>20136</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Viale Bligny 3, 20136 Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4ea546ad490102dac3c6f318</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Soul Food</td>
      <td>Food &amp; Drink Shop</td>
      <td>Via Gola 3</td>
      <td>NaN</td>
      <td>45.449015</td>
      <td>9.176673</td>
      <td>[{'label': 'display', 'lat': 45.44901511031179...</td>
      <td>506</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Gola 3, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4f5b9d25e4b06784f7be1bf8</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Free Art Cafè</td>
      <td>Bar</td>
      <td>Vigevano, 9</td>
      <td>NaN</td>
      <td>45.453114</td>
      <td>9.174698</td>
      <td>[{'label': 'display', 'lat': 45.453114, 'lng':...</td>
      <td>391</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Vigevano, 9, Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4c2a5f4ec758e21e99883a3f</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Volutta Café</td>
      <td>Café</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.463032</td>
      <td>9.188423</td>
      <td>[{'label': 'display', 'lat': 45.46303176460675...</td>
      <td>1304</td>
      <td>NaN</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Milano Lombardia, Italia]</td>
      <td>NaN</td>
      <td>4e05d52e45ddb2875c400801</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Jade Cafè</td>
      <td>Asian Restaurant</td>
      <td>Via Palazzo Reale 5</td>
      <td>NaN</td>
      <td>45.462479</td>
      <td>9.192617</td>
      <td>[{'label': 'display', 'lat': 45.46247899046734...</td>
      <td>1456</td>
      <td>20122</td>
      <td>IT</td>
      <td>Milano</td>
      <td>Lombardia</td>
      <td>Italia</td>
      <td>[Via Palazzo Reale 5, 20122 Milano Lombardia, ...</td>
      <td>NaN</td>
      <td>4bd03897caff9521825fcef0</td>
    </tr>
  </tbody>
</table>
</div>




```python
venues_map = folium.Map(location=[latitude, longitude], zoom_start=15) # generate map centred around Porta Ticinese


# add landmark as a red circle mark
folium.features.CircleMarker(
    [latitude, longitude],
    radius=10,
    popup='Arco di Porta Ticinese',
    fill=True,
    color='red',
    fill_color='red',
    fill_opacity=0.6
    ).add_to(venues_map)


# add spots to the map as blue circle markers
for lat, lng, label in zip(dataframe_filtered.lat, dataframe_filtered.lng, dataframe_filtered.categories):
    folium.features.CircleMarker(
        [lat, lng],
        radius=5,
        popup=label,
        fill=True,
        color='blue',
        fill_color='blue',
        fill_opacity=0.6
        ).add_to(venues_map)

# display map
venues_map
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe src="about:blank" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" data-html=PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdnaXQuY29tL3B5dGhvbi12aXN1YWxpemF0aW9uL2ZvbGl1bS9tYXN0ZXIvZm9saXVtL3RlbXBsYXRlcy9sZWFmbGV0LmF3ZXNvbWUucm90YXRlLmNzcyIvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlIiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZScsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbNDUuNDUzMDMxNCw5LjE3OTcxMTFdLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgem9vbTogMTUsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBtYXhCb3VuZHM6IGJvdW5kcywKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGxheWVyczogW10sCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB3b3JsZENvcHlKdW1wOiBmYWxzZSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGNyczogTC5DUlMuRVBTRzM4NTcKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgfSk7CiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciB0aWxlX2xheWVyXzZmOTE5ZjQzNzNkNzQwYzFiZjE5MWNiNjA3NmI5NDBiID0gTC50aWxlTGF5ZXIoCiAgICAgICAgICAgICAgICAnaHR0cHM6Ly97c30udGlsZS5vcGVuc3RyZWV0bWFwLm9yZy97en0ve3h9L3t5fS5wbmcnLAogICAgICAgICAgICAgICAgewogICJhdHRyaWJ1dGlvbiI6IG51bGwsCiAgImRldGVjdFJldGluYSI6IGZhbHNlLAogICJtYXhab29tIjogMTgsCiAgIm1pblpvb20iOiAxLAogICJub1dyYXAiOiBmYWxzZSwKICAic3ViZG9tYWlucyI6ICJhYmMiCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80NmIyY2ZjM2M5ZjQ0NTM3OGE4OWNhODZmZjliMDAwZCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ1MzAzMTQsOS4xNzk3MTExXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogInJlZCIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogInJlZCIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogMTAsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNjU5YmMyYTViN2I3NGY0Nzk3ZjM3YTYxMmIwOTBhMGQgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNmUzYjAyNjA2YjNiNGViNThjMmVkNTZjYzljNTg5ZjMgPSAkKCc8ZGl2IGlkPSJodG1sXzZlM2IwMjYwNmIzYjRlYjU4YzJlZDU2Y2M5YzU4OWYzIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5BcmNvIGRpIFBvcnRhIFRpY2luZXNlPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF82NTliYzJhNWI3Yjc0ZjQ3OTdmMzdhNjEyYjA5MGEwZC5zZXRDb250ZW50KGh0bWxfNmUzYjAyNjA2YjNiNGViNThjMmVkNTZjYzljNTg5ZjMpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNDZiMmNmYzNjOWY0NDUzNzhhODljYTg2ZmY5YjAwMGQuYmluZFBvcHVwKHBvcHVwXzY1OWJjMmE1YjdiNzRmNDc5N2YzN2E2MTJiMDkwYTBkKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzYwN2ZlYWRiYzRiMzQwNjlhM2Q4MjAwNzIwZGY4YzVhID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDUzMjQzMDQyNDE2MDEsOS4xODAzNzAyNDI2MTUwMThdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMjJlN2FiOTcyNjY1NGU1YmI0Y2JkZmU0NDBhOGVkNDIgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNWNlMGM4Zjc0Mjk0NDA5NmFjOThiZWQ0ZTIzZjdkNDkgPSAkKCc8ZGl2IGlkPSJodG1sXzVjZTBjOGY3NDI5NDQwOTZhYzk4YmVkNGUyM2Y3ZDQ5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5HYXN0cm9wdWI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzIyZTdhYjk3MjY2NTRlNWJiNGNiZGZlNDQwYThlZDQyLnNldENvbnRlbnQoaHRtbF81Y2UwYzhmNzQyOTQ0MDk2YWM5OGJlZDRlMjNmN2Q0OSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl82MDdmZWFkYmM0YjM0MDY5YTNkODIwMDcyMGRmOGM1YS5iaW5kUG9wdXAocG9wdXBfMjJlN2FiOTcyNjY1NGU1YmI0Y2JkZmU0NDBhOGVkNDIpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMjdkMGYyYzU2ODdmNDNiOGFiNjM1ZWZkZTliZjMwNmIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTI4MTgzOTU1OTAwNSw5LjE3ODc5NjAwNDEwNjQ4XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzYxZTdmYzYxYTM2ODQ4MWJhNmEzYzdkMGNkYjQ5YWQ4ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzBkYzM5MTdiODY5NTQxYjc4ZjRmYmY0Nzc1MDIyNDI1ID0gJCgnPGRpdiBpZD0iaHRtbF8wZGMzOTE3Yjg2OTU0MWI3OGY0ZmJmNDc3NTAyMjQyNSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2Fmw6k8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzYxZTdmYzYxYTM2ODQ4MWJhNmEzYzdkMGNkYjQ5YWQ4LnNldENvbnRlbnQoaHRtbF8wZGMzOTE3Yjg2OTU0MWI3OGY0ZmJmNDc3NTAyMjQyNSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8yN2QwZjJjNTY4N2Y0M2I4YWI2MzVlZmRlOWJmMzA2Yi5iaW5kUG9wdXAocG9wdXBfNjFlN2ZjNjFhMzY4NDgxYmE2YTNjN2QwY2RiNDlhZDgpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNzUzN2Q2ZmMzMDc0NDA4MDhhMDM4YmI5OGQwOTU4MTQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTg4NjYzNzk0NTEyNiw5LjE3MTE1OTI2NzQyNTUzN10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF81NWQxOTMxMWQ5NDI0NjRlOTFkYzUzOTkzZGE3ZjgxMSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF81MzQ1MjBjNzE2MTA0MDJhYjNlZGEyNmM2OWE5YTIzNiA9ICQoJzxkaXYgaWQ9Imh0bWxfNTM0NTIwYzcxNjEwNDAyYWIzZWRhMjZjNjlhOWEyMzYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkdyb2NlcnkgU3RvcmU8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzU1ZDE5MzExZDk0MjQ2NGU5MWRjNTM5OTNkYTdmODExLnNldENvbnRlbnQoaHRtbF81MzQ1MjBjNzE2MTA0MDJhYjNlZGEyNmM2OWE5YTIzNik7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl83NTM3ZDZmYzMwNzQ0MDgwOGEwMzhiYjk4ZDA5NTgxNC5iaW5kUG9wdXAocG9wdXBfNTVkMTkzMTFkOTQyNDY0ZTkxZGM1Mzk5M2RhN2Y4MTEpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfY2M5MGY4YTI0OGRjNDc0ZDkxZjBmZjFjNzZiYTdhNmYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTIxOTA3MzcwNTg2MTUsOS4xODE5ODE5MTgyOTEwNjNdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfOTNlYzZjNGI3NDY2NDE2NmEyNTE2MDkzN2FkMDUwN2QgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNTY0ZGJlYzdkMTg0NDViMzk2ZDJjY2E2ZDg3MTgyNzUgPSAkKCc8ZGl2IGlkPSJodG1sXzU2NGRiZWM3ZDE4NDQ1YjM5NmQyY2NhNmQ4NzE4Mjc1IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5QdWI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzkzZWM2YzRiNzQ2NjQxNjZhMjUxNjA5MzdhZDA1MDdkLnNldENvbnRlbnQoaHRtbF81NjRkYmVjN2QxODQ0NWIzOTZkMmNjYTZkODcxODI3NSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9jYzkwZjhhMjQ4ZGM0NzRkOTFmMGZmMWM3NmJhN2E2Zi5iaW5kUG9wdXAocG9wdXBfOTNlYzZjNGI3NDY2NDE2NmEyNTE2MDkzN2FkMDUwN2QpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMTk2NDk2ZmNhZGJjNDMyZjk5N2UwZDIxOGViN2EwMmIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTI0MDc2Mzk0MzI2NCw5LjE3ODgyMjYzMTUxNDk1M10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF85NzYxYjUyODc5NzI0YTNkOWM3ZWI1ZTMwNGI1MTVmMiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9lZjFkY2Q5ZGMxODU0OGRmODZlNDk2Zjg0OWEyMDI1OSA9ICQoJzxkaXYgaWQ9Imh0bWxfZWYxZGNkOWRjMTg1NDhkZjg2ZTQ5NmY4NDlhMjAyNTkiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkJhcjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfOTc2MWI1Mjg3OTcyNGEzZDljN2ViNWUzMDRiNTE1ZjIuc2V0Q29udGVudChodG1sX2VmMWRjZDlkYzE4NTQ4ZGY4NmU0OTZmODQ5YTIwMjU5KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzE5NjQ5NmZjYWRiYzQzMmY5OTdlMGQyMThlYjdhMDJiLmJpbmRQb3B1cChwb3B1cF85NzYxYjUyODc5NzI0YTNkOWM3ZWI1ZTMwNGI1MTVmMik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9lMzBhMjE1YzhlNGU0NDUxODk0OWRkNjhjMWQ2NmUxMyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ1MDk0MjU3MDQzNDQ2LDkuMTg0MTI1NzcyMjgwMzQ4XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2I2YzQ3ZDI1ZjM3ZjQ2YWJiZmY0ODE5NTY4ZTkzNWYzID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2U1Njc2YWFlMDM0ZTRmMWQ4Mjg2ZWVmZjQ5MGI3NDQ4ID0gJCgnPGRpdiBpZD0iaHRtbF9lNTY3NmFhZTAzNGU0ZjFkODI4NmVlZmY0OTBiNzQ0OCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RXZlbnQgU3BhY2U8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2I2YzQ3ZDI1ZjM3ZjQ2YWJiZmY0ODE5NTY4ZTkzNWYzLnNldENvbnRlbnQoaHRtbF9lNTY3NmFhZTAzNGU0ZjFkODI4NmVlZmY0OTBiNzQ0OCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9lMzBhMjE1YzhlNGU0NDUxODk0OWRkNjhjMWQ2NmUxMy5iaW5kUG9wdXAocG9wdXBfYjZjNDdkMjVmMzdmNDZhYmJmZjQ4MTk1NjhlOTM1ZjMpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZjAzOWQ0MDM4ZTA1NDc5OWEzMWVmNzlhOTY0ZDcwNGUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTEzMDEsOS4xNzM0MjhdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfY2EyODA5NDBkYWNjNDIwYzhjYzgzOThhZThjNWYwYTAgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNDBlNjA2NTQzOTZkNDMwY2E3OGJiYzRjZTNjZWY4YzQgPSAkKCc8ZGl2IGlkPSJodG1sXzQwZTYwNjU0Mzk2ZDQzMGNhNzhiYmM0Y2UzY2VmOGM0IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Db2NrdGFpbCBCYXI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2NhMjgwOTQwZGFjYzQyMGM4Y2M4Mzk4YWU4YzVmMGEwLnNldENvbnRlbnQoaHRtbF80MGU2MDY1NDM5NmQ0MzBjYTc4YmJjNGNlM2NlZjhjNCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9mMDM5ZDQwMzhlMDU0Nzk5YTMxZWY3OWE5NjRkNzA0ZS5iaW5kUG9wdXAocG9wdXBfY2EyODA5NDBkYWNjNDIwYzhjYzgzOThhZThjNWYwYTApOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMTU5NDQ2YmJkYjY1NGEzYmIyZjI1NDc4N2Y5Y2E3NzUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTIwMzI4NzI3OTMzOCw5LjE3NjcxNjgwNDUwNDM5M10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF84NDA3YzJkNGYzNDY0OWI1YWU4MjE5NDQ3MDNmNDA1ZiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8xNzU4ZTBlMzRjNjQ0ZjBhYmI3YzgxYTA2MTljNWY2ZSA9ICQoJzxkaXYgaWQ9Imh0bWxfMTc1OGUwZTM0YzY0NGYwYWJiN2M4MWEwNjE5YzVmNmUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNvY2t0YWlsIEJhcjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfODQwN2MyZDRmMzQ2NDliNWFlODIxOTQ0NzAzZjQwNWYuc2V0Q29udGVudChodG1sXzE3NThlMGUzNGM2NDRmMGFiYjdjODFhMDYxOWM1ZjZlKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzE1OTQ0NmJiZGI2NTRhM2JiMmYyNTQ3ODdmOWNhNzc1LmJpbmRQb3B1cChwb3B1cF84NDA3YzJkNGYzNDY0OWI1YWU4MjE5NDQ3MDNmNDA1Zik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80Y2FkN2ZiNTI1ZjQ0ZThiOTY1OTU0NTNjMDFmNDEyOCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ2NDg0NjQyODc1ODY1NSw5LjE5MTc5NTY1NTM5NzUwMl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9hYjUwMDA3NTc0YTE0ZDA4YTc5YjllYjAxZjA0OWNhOSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF80NTM3NDhhYTM5ODA0OTM4OWM0ZDFiNzhmYjc1NTc1ZCA9ICQoJzxkaXYgaWQ9Imh0bWxfNDUzNzQ4YWEzOTgwNDkzODljNGQxYjc4ZmI3NTU3NWQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkdvdXJtZXQgU2hvcDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfYWI1MDAwNzU3NGExNGQwOGE3OWI5ZWIwMWYwNDljYTkuc2V0Q29udGVudChodG1sXzQ1Mzc0OGFhMzk4MDQ5Mzg5YzRkMWI3OGZiNzU1NzVkKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzRjYWQ3ZmI1MjVmNDRlOGI5NjU5NTQ1M2MwMWY0MTI4LmJpbmRQb3B1cChwb3B1cF9hYjUwMDA3NTc0YTE0ZDA4YTc5YjllYjAxZjA0OWNhOSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9iMzEzZDZlNGRhYzM0MGU2YWQ5OWQ4OWJiNjJhZmNkMiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ0ODc2NzYzNjgxNTQyNSw5LjE3NzI2MTU2NDIxNTI4Nl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9lMmJmZWFjZTE4OGE0MjUwOGRlOTQwYTNiY2YwNDEwYiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF81ZjJhN2MxZTNhYzE0MDMwYjFhNWFhYWU3NTFmYzcyNCA9ICQoJzxkaXYgaWQ9Imh0bWxfNWYyYTdjMWUzYWMxNDAzMGIxYTVhYWFlNzUxZmM3MjQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNvY2t0YWlsIEJhcjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZTJiZmVhY2UxODhhNDI1MDhkZTk0MGEzYmNmMDQxMGIuc2V0Q29udGVudChodG1sXzVmMmE3YzFlM2FjMTQwMzBiMWE1YWFhZTc1MWZjNzI0KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2IzMTNkNmU0ZGFjMzQwZTZhZDk5ZDg5YmI2MmFmY2QyLmJpbmRQb3B1cChwb3B1cF9lMmJmZWFjZTE4OGE0MjUwOGRlOTQwYTNiY2YwNDEwYik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81YjE0NTU4YTYxYTY0OTZiODIzNzliMmEyNTY1NGVjYSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ2MjI4LDkuMTk0MzhdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfZjcyODFlNmU1OGFhNGZmMTlkODM1MTU2MmU0OWJmNzcgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfZTVkYTViN2QzODYyNDZiM2EzYTZiZDNiZmQxM2Y5NjcgPSAkKCc8ZGl2IGlkPSJodG1sX2U1ZGE1YjdkMzg2MjQ2YjNhM2E2YmQzYmZkMTNmOTY3IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5SZXN0YXVyYW50PC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9mNzI4MWU2ZTU4YWE0ZmYxOWQ4MzUxNTYyZTQ5YmY3Ny5zZXRDb250ZW50KGh0bWxfZTVkYTViN2QzODYyNDZiM2EzYTZiZDNiZmQxM2Y5NjcpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNWIxNDU1OGE2MWE2NDk2YjgyMzc5YjJhMjU2NTRlY2EuYmluZFBvcHVwKHBvcHVwX2Y3MjgxZTZlNThhYTRmZjE5ZDgzNTE1NjJlNDliZjc3KTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzBjNDNjNjg4YzY0ZjQ4YmY4YmFjNGUzZDY2YTFhOTNlID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDQ2ODUxNzU3NTc1MjcsOS4xNzkzOTc0Nzg2NTkwNDVdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfOGU5OTYzNmM2Mjg5NDJmMTg0ZmVjODk5MjM0YjUyYmUgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfYzhjNDU3NDI0Mzk4NDQyNmJhMWYzNmYyNGQ3MjBiMDIgPSAkKCc8ZGl2IGlkPSJodG1sX2M4YzQ1NzQyNDM5ODQ0MjZiYTFmMzZmMjRkNzIwYjAyIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DYWbDqTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfOGU5OTYzNmM2Mjg5NDJmMTg0ZmVjODk5MjM0YjUyYmUuc2V0Q29udGVudChodG1sX2M4YzQ1NzQyNDM5ODQ0MjZiYTFmMzZmMjRkNzIwYjAyKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzBjNDNjNjg4YzY0ZjQ4YmY4YmFjNGUzZDY2YTFhOTNlLmJpbmRQb3B1cChwb3B1cF84ZTk5NjM2YzYyODk0MmYxODRmZWM4OTkyMzRiNTJiZSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9lZTc5MDZjOTdlMTk0NzUwYTUxMjQ0YjYyMGMwN2IyNCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ2MDE5NzkxNTU4ODkzNSw5LjE3NzE0MjM3OTk1NTk5N10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9jZTI2MzEwNDFmZDA0NTVkYWQxOGQ5M2NhY2YzNGY4YyA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8xOTdjZWYyNjYyYWE0ZjQ4ODNmNTRjYWQ4NzJiYTIyOSA9ICQoJzxkaXYgaWQ9Imh0bWxfMTk3Y2VmMjY2MmFhNGY0ODgzZjU0Y2FkODcyYmEyMjkiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNhZsOpPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9jZTI2MzEwNDFmZDA0NTVkYWQxOGQ5M2NhY2YzNGY4Yy5zZXRDb250ZW50KGh0bWxfMTk3Y2VmMjY2MmFhNGY0ODgzZjU0Y2FkODcyYmEyMjkpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfZWU3OTA2Yzk3ZTE5NDc1MGE1MTI0NGI2MjBjMDdiMjQuYmluZFBvcHVwKHBvcHVwX2NlMjYzMTA0MWZkMDQ1NWRhZDE4ZDkzY2FjZjM0ZjhjKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzI5Mjc5YmNkMTVmYzQxNTNhOTFlOGY4ZDJiMTk0NWE0ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDUsOS4xN10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9lODE5ODZjMzM3NGM0YmFjOWI4NDljOTBhM2Q1ZjE4YyA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9iOGQ3OGM2ZDNmNjU0MGEwOWJhZjc1YTE1OWE5ZDg5MyA9ICQoJzxkaXYgaWQ9Imh0bWxfYjhkNzhjNmQzZjY1NDBhMDliYWY3NWExNTlhOWQ4OTMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlJlc3RhdXJhbnQ8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2U4MTk4NmMzMzc0YzRiYWM5Yjg0OWM5MGEzZDVmMThjLnNldENvbnRlbnQoaHRtbF9iOGQ3OGM2ZDNmNjU0MGEwOWJhZjc1YTE1OWE5ZDg5Myk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8yOTI3OWJjZDE1ZmM0MTUzYTkxZThmOGQyYjE5NDVhNC5iaW5kUG9wdXAocG9wdXBfZTgxOTg2YzMzNzRjNGJhYzliODQ5YzkwYTNkNWYxOGMpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfODY2YzcxYTM0NDg0NDRjNGEyYjQ3YmE3NDllYjc0M2YgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NDM4MTAxOTM2MzY0NDUsOS4xODExNDA1NTUxMTE5XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzg2NmYwNzkwMWI0MDRhYjA5NzlmZGNjMGJhNTRiM2I0ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2Q1ZDU5YzBiMzVkOTRiYmRiZTIyNWU2NDA5NWI1ZWE1ID0gJCgnPGRpdiBpZD0iaHRtbF9kNWQ1OWMwYjM1ZDk0YmJkYmUyMjVlNjQwOTViNWVhNSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2Fmw6k8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzg2NmYwNzkwMWI0MDRhYjA5NzlmZGNjMGJhNTRiM2I0LnNldENvbnRlbnQoaHRtbF9kNWQ1OWMwYjM1ZDk0YmJkYmUyMjVlNjQwOTViNWVhNSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl84NjZjNzFhMzQ0ODQ0NGM0YTJiNDdiYTc0OWViNzQzZi5iaW5kUG9wdXAocG9wdXBfODY2ZjA3OTAxYjQwNGFiMDk3OWZkY2MwYmE1NGIzYjQpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYmMxNDMyNGNhZDM4NDI4M2JhODgwYjllZjgzMjAzOTkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTI5Mzg5NjMwMzU3NCw5LjE2NzQyMTEyNjI3NDEyM10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF82ZDQ5ZWQzMTZlNjQ0YTY2YmUwYzVjOTk3ZGVjNjY2YyA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF85NDA0MTVhNWFmYTc0MTU5YmQyMTQ4YTJmYWNhMTVkMSA9ICQoJzxkaXYgaWQ9Imh0bWxfOTQwNDE1YTVhZmE3NDE1OWJkMjE0OGEyZmFjYTE1ZDEiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkdlbmVyYWwgRW50ZXJ0YWlubWVudDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfNmQ0OWVkMzE2ZTY0NGE2NmJlMGM1Yzk5N2RlYzY2NmMuc2V0Q29udGVudChodG1sXzk0MDQxNWE1YWZhNzQxNTliZDIxNDhhMmZhY2ExNWQxKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2JjMTQzMjRjYWQzODQyODNiYTg4MGI5ZWY4MzIwMzk5LmJpbmRQb3B1cChwb3B1cF82ZDQ5ZWQzMTZlNjQ0YTY2YmUwYzVjOTk3ZGVjNjY2Yyk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl84MmRjNzE3YmEwNmI0MmUwYWNiNjRkN2Y2NWI5YjJhNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ0NjkxNjU0MjQ5NDIzNiw5LjE3OTQ0NjQ2MDg2Mzk2OF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF8yYjhhYjk5ZWJhYjk0M2I4YmMxZTFhN2ZkMDUzM2QxZCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8yNWVhN2Y0YWM4MTI0YTAxYjk4M2RiZjM2ZjA3M2Q4ZSA9ICQoJzxkaXYgaWQ9Imh0bWxfMjVlYTdmNGFjODEyNGEwMWI5ODNkYmYzNmYwNzNkOGUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkJhcjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfMmI4YWI5OWViYWI5NDNiOGJjMWUxYTdmZDA1MzNkMWQuc2V0Q29udGVudChodG1sXzI1ZWE3ZjRhYzgxMjRhMDFiOTgzZGJmMzZmMDczZDhlKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzgyZGM3MTdiYTA2YjQyZTBhY2I2NGQ3ZjY1YjliMmE2LmJpbmRQb3B1cChwb3B1cF8yYjhhYjk5ZWJhYjk0M2I4YmMxZTFhN2ZkMDUzM2QxZCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9iZTQwZTNhNmQ1OGY0YmZmOGQ4YmFlNTRlOGE3M2VlYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ1ODkyMyw5LjE4MjYyXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2U2ZmVhZDYwOTYxZjRiZDI5MzIzNjBhN2ZjOGI1ZWEyID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzZlMzc2ZTlhMGY3OTQ2MTViN2JlMDJhYWMyMTZhYTcwID0gJCgnPGRpdiBpZD0iaHRtbF82ZTM3NmU5YTBmNzk0NjE1YjdiZTAyYWFjMjE2YWE3MCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2FyaWJiZWFuIFJlc3RhdXJhbnQ8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2U2ZmVhZDYwOTYxZjRiZDI5MzIzNjBhN2ZjOGI1ZWEyLnNldENvbnRlbnQoaHRtbF82ZTM3NmU5YTBmNzk0NjE1YjdiZTAyYWFjMjE2YWE3MCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9iZTQwZTNhNmQ1OGY0YmZmOGQ4YmFlNTRlOGE3M2VlYi5iaW5kUG9wdXAocG9wdXBfZTZmZWFkNjA5NjFmNGJkMjkzMjM2MGE3ZmM4YjVlYTIpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMmFlMzlhYTQ3MDcyNGQ5ZmE4ZmZiZTg5NGYwOWVkMGQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTM0MDQ2ODc0MzA4NSw5LjE2NzI0MzY2OTE4MzY0XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2NjOTM3ZGRjZDAyMjRjMWY5NjM1ZDI0MGQ4NDI2MDIwID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2IwM2U3MGM4NTQ2MTQwOTNhMzhmZTJjM2Q4NzkzNzRlID0gJCgnPGRpdiBpZD0iaHRtbF9iMDNlNzBjODU0NjE0MDkzYTM4ZmUyYzNkODc5Mzc0ZSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+R2VuZXJhbCBFbnRlcnRhaW5tZW50PC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9jYzkzN2RkY2QwMjI0YzFmOTYzNWQyNDBkODQyNjAyMC5zZXRDb250ZW50KGh0bWxfYjAzZTcwYzg1NDYxNDA5M2EzOGZlMmMzZDg3OTM3NGUpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfMmFlMzlhYTQ3MDcyNGQ5ZmE4ZmZiZTg5NGYwOWVkMGQuYmluZFBvcHVwKHBvcHVwX2NjOTM3ZGRjZDAyMjRjMWY5NjM1ZDI0MGQ4NDI2MDIwKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2IwZjhiMWQ1Y2ZlYjQyZTI5NGM5YmI0NmIwZDMyNzcxID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDQ3NjMxOTY3Njc5NTA2LDkuMTc3MTA1OTg5NzAzNzkyXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2Q2ZDkzMTA1NWE2ZDRlYjdiZmI0NGE5YTJjZWEyMjczID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2YzNDFhZjllNzRlOTQ0OWE5Y2IxNmJkY2M4MWFiNWEwID0gJCgnPGRpdiBpZD0iaHRtbF9mMzQxYWY5ZTc0ZTk0NDlhOWNiMTZiZGNjODFhYjVhMCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q29ja3RhaWwgQmFyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9kNmQ5MzEwNTVhNmQ0ZWI3YmZiNDRhOWEyY2VhMjI3My5zZXRDb250ZW50KGh0bWxfZjM0MWFmOWU3NGU5NDQ5YTljYjE2YmRjYzgxYWI1YTApOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfYjBmOGIxZDVjZmViNDJlMjk0YzliYjQ2YjBkMzI3NzEuYmluZFBvcHVwKHBvcHVwX2Q2ZDkzMTA1NWE2ZDRlYjdiZmI0NGE5YTJjZWEyMjczKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2M3NzMzNGYwMDFhODQ4YjI5MDY3M2QzMzNkNWJlMzcwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDUyMTg3NzYxMzU5MSw5LjE4MTg5NzI3MDExNTI1Ml0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF80NzUxZTc1YTRjMDY0ZmY0YjczODZmYTIyYzk2OGViNCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8yYTY4YzM3OThiOTY0NzY2OTljNGY1OTE3MTlkMzM5ZCA9ICQoJzxkaXYgaWQ9Imh0bWxfMmE2OGMzNzk4Yjk2NDc2Njk5YzRmNTkxNzE5ZDMzOWQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkJhcjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfNDc1MWU3NWE0YzA2NGZmNGI3Mzg2ZmEyMmM5NjhlYjQuc2V0Q29udGVudChodG1sXzJhNjhjMzc5OGI5NjQ3NjY5OWM0ZjU5MTcxOWQzMzlkKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2M3NzMzNGYwMDFhODQ4YjI5MDY3M2QzMzNkNWJlMzcwLmJpbmRQb3B1cChwb3B1cF80NzUxZTc1YTRjMDY0ZmY0YjczODZmYTIyYzk2OGViNCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8wZDAwOTFkNTQxNjk0ZWJhOWQ1ODUwY2NhOWRhZTQ2OCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ1MTEzMiw5LjE3MTIyMl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF8wNTI3N2FkYzk1Mzc0NTA3YTE2MjIxNGJmMzYzNGEzOSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF84YTU3NTg2OTBhOGM0YjUwOWIzMWVjMjZmM2Y4NTg4MiA9ICQoJzxkaXYgaWQ9Imh0bWxfOGE1NzU4NjkwYThjNGI1MDliMzFlYzI2ZjNmODU4ODIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNvY2t0YWlsIEJhcjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfMDUyNzdhZGM5NTM3NDUwN2ExNjIyMTRiZjM2MzRhMzkuc2V0Q29udGVudChodG1sXzhhNTc1ODY5MGE4YzRiNTA5YjMxZWMyNmYzZjg1ODgyKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzBkMDA5MWQ1NDE2OTRlYmE5ZDU4NTBjY2E5ZGFlNDY4LmJpbmRQb3B1cChwb3B1cF8wNTI3N2FkYzk1Mzc0NTA3YTE2MjIxNGJmMzYzNGEzOSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9hNjI1OTFjMTA0YjE0NWUwYmE0ZDJlMTQxMDM2ZjEzYSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ2MDQyNjE4MDkyMzg0LDkuMTg4NDI3MDg2OTcwMDk4XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzFjMGRmNWM5Mzg0MDQ3MjViZmU0NWMyZGQwY2NjZmZlID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzg5OTQ5ZDRhNWI0NzQ2NjViZmYxNDZmNmVjMjFmNTNiID0gJCgnPGRpdiBpZD0iaHRtbF84OTk0OWQ0YTViNDc0NjY1YmZmMTQ2ZjZlYzIxZjUzYiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2Fmw6k8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzFjMGRmNWM5Mzg0MDQ3MjViZmU0NWMyZGQwY2NjZmZlLnNldENvbnRlbnQoaHRtbF84OTk0OWQ0YTViNDc0NjY1YmZmMTQ2ZjZlYzIxZjUzYik7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9hNjI1OTFjMTA0YjE0NWUwYmE0ZDJlMTQxMDM2ZjEzYS5iaW5kUG9wdXAocG9wdXBfMWMwZGY1YzkzODQwNDcyNWJmZTQ1YzJkZDBjY2NmZmUpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMDYwMGQ3MTViZDE0NDcyOWEwNjg4MmUyNjc4MDNmOGIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTQ3NjA2ODEzMjUxNyw5LjE4MDU3NDgwMTQwODE0N10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9iN2FiNDgyYmMzNDc0MTViYWM2YzZkNjUyZDgwOGY1ZSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF82MzJmZmExZGY4NjY0MTE4YjFlMWViZWU4OTNjNjQ0ZiA9ICQoJzxkaXYgaWQ9Imh0bWxfNjMyZmZhMWRmODY2NDExOGIxZTFlYmVlODkzYzY0NGYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNhZsOpPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9iN2FiNDgyYmMzNDc0MTViYWM2YzZkNjUyZDgwOGY1ZS5zZXRDb250ZW50KGh0bWxfNjMyZmZhMWRmODY2NDExOGIxZTFlYmVlODkzYzY0NGYpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfMDYwMGQ3MTViZDE0NDcyOWEwNjg4MmUyNjc4MDNmOGIuYmluZFBvcHVwKHBvcHVwX2I3YWI0ODJiYzM0NzQxNWJhYzZjNmQ2NTJkODA4ZjVlKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzFhZTNhNTBhMDI0MTQxNTE5NmMzNDI3NzlmZTcxZmZiID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDUyMTA4LDkuMTgyNTcyXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzZmZmE4ZDllMWVkZDRkOGJiZGEzMjZlNWQ1M2M0MTZlID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2Y4YjFjNTRmY2JlMDQzMTRhYWI4NTY2NzA1OGNiMjc0ID0gJCgnPGRpdiBpZD0iaHRtbF9mOGIxYzU0ZmNiZTA0MzE0YWFiODU2NjcwNThjYjI3NCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2Fmw6k8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzZmZmE4ZDllMWVkZDRkOGJiZGEzMjZlNWQ1M2M0MTZlLnNldENvbnRlbnQoaHRtbF9mOGIxYzU0ZmNiZTA0MzE0YWFiODU2NjcwNThjYjI3NCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8xYWUzYTUwYTAyNDE0MTUxOTZjMzQyNzc5ZmU3MWZmYi5iaW5kUG9wdXAocG9wdXBfNmZmYThkOWUxZWRkNGQ4YmJkYTMyNmU1ZDUzYzQxNmUpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfY2VmMTQ5ZDA5MWUxNGFkZmExZDQ3N2FmNjNlMWY1MmYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTQ2OSw5LjE5ODE5XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2QwODQ0MmRkM2EzZTQwMDE4ZGFiMjJlODBiYzUzNDI2ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzI4NzY1ZWM4OGRlMjQxNDRiOGEwMGMwN2U2YjUxY2Y0ID0gJCgnPGRpdiBpZD0iaHRtbF8yODc2NWVjODhkZTI0MTQ0YjhhMDBjMDdlNmI1MWNmNCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGluZXI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2QwODQ0MmRkM2EzZTQwMDE4ZGFiMjJlODBiYzUzNDI2LnNldENvbnRlbnQoaHRtbF8yODc2NWVjODhkZTI0MTQ0YjhhMDBjMDdlNmI1MWNmNCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9jZWYxNDlkMDkxZTE0YWRmYTFkNDc3YWY2M2UxZjUyZi5iaW5kUG9wdXAocG9wdXBfZDA4NDQyZGQzYTNlNDAwMThkYWIyMmU4MGJjNTM0MjYpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYTQ1Mjg2YzBjOTYzNDE1ZGI1M2YxODQyODc2OGUyNDYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NjIyNTI1LDkuMTg5NTA3NF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF84Mjg4ZDgyMzBjMDQ0YWZjODVhN2ExYTFhNmVlMDc1OCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9kMzE0YzJhYTIwNWY0MTZhYmIxZGNhYjJiODMwNmQ0NiA9ICQoJzxkaXYgaWQ9Imh0bWxfZDMxNGMyYWEyMDVmNDE2YWJiMWRjYWIyYjgzMDZkNDYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhlYWx0aCBGb29kIFN0b3JlPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF84Mjg4ZDgyMzBjMDQ0YWZjODVhN2ExYTFhNmVlMDc1OC5zZXRDb250ZW50KGh0bWxfZDMxNGMyYWEyMDVmNDE2YWJiMWRjYWIyYjgzMDZkNDYpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfYTQ1Mjg2YzBjOTYzNDE1ZGI1M2YxODQyODc2OGUyNDYuYmluZFBvcHVwKHBvcHVwXzgyODhkODIzMGMwNDRhZmM4NWE3YTFhMWE2ZWUwNzU4KTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2E2NzllYWQ3MDYxMDQ0MTlhYzAxYjA0MTQwMzQ0M2Y5ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDU3ODE5MDQ1MjUzNDUsOS4xODEwOTk1NjIwNDkxODZdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMWM1ZTlhNWUwNDcwNGQ5YWI2ODc4MjIwMmIxYTNmZDUgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNGNhYTQ2ODIzZDAzNDQ4ZmE3NzFlMDY5MDA1ODk5Y2MgPSAkKCc8ZGl2IGlkPSJodG1sXzRjYWE0NjgyM2QwMzQ0OGZhNzcxZTA2OTAwNTg5OWNjIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Db2NrdGFpbCBCYXI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzFjNWU5YTVlMDQ3MDRkOWFiNjg3ODIyMDJiMWEzZmQ1LnNldENvbnRlbnQoaHRtbF80Y2FhNDY4MjNkMDM0NDhmYTc3MWUwNjkwMDU4OTljYyk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9hNjc5ZWFkNzA2MTA0NDE5YWMwMWIwNDE0MDM0NDNmOS5iaW5kUG9wdXAocG9wdXBfMWM1ZTlhNWUwNDcwNGQ5YWI2ODc4MjIwMmIxYTNmZDUpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNjUwNDdkMmVkODE4NGVjMTk3OTE5NWE3ODczOGQzYWUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTIyMzYsOS4xODMxMTddLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNzc5MGFjOWNmYjZmNDI5MTgyZmZlZTQ2ZDQ3ODQyOTcgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfOGVhODhlNGI2OWI0NDJkOWExYjVlNGViYTM5NzIxYmIgPSAkKCc8ZGl2IGlkPSJodG1sXzhlYTg4ZTRiNjliNDQyZDlhMWI1ZTRlYmEzOTcyMWJiIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5KYXBhbmVzZSBSZXN0YXVyYW50PC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF83NzkwYWM5Y2ZiNmY0MjkxODJmZmVlNDZkNDc4NDI5Ny5zZXRDb250ZW50KGh0bWxfOGVhODhlNGI2OWI0NDJkOWExYjVlNGViYTM5NzIxYmIpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNjUwNDdkMmVkODE4NGVjMTk3OTE5NWE3ODczOGQzYWUuYmluZFBvcHVwKHBvcHVwXzc3OTBhYzljZmI2ZjQyOTE4MmZmZWU0NmQ0Nzg0Mjk3KTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2MxZmVjMWM2ZjEwMDRmZTRhZGE0NGQ4NjRiZjdhMDcwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDQ3NDQzMzM5MjA2MDk2LDkuMTc3MjgzNTU5NTM4Mzg2XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2U0YTM0MzE1NTAwZTQ2MjE5YzRlNWNlYWUyYmIyNGM2ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2Q0MjQxZjNjYjU2ODRjOTRhYTYwZDMxZGI4Y2NlOTIyID0gJCgnPGRpdiBpZD0iaHRtbF9kNDI0MWYzY2I1Njg0Yzk0YWE2MGQzMWRiOGNjZTkyMiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QmFyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9lNGEzNDMxNTUwMGU0NjIxOWM0ZTVjZWFlMmJiMjRjNi5zZXRDb250ZW50KGh0bWxfZDQyNDFmM2NiNTY4NGM5NGFhNjBkMzFkYjhjY2U5MjIpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfYzFmZWMxYzZmMTAwNGZlNGFkYTQ0ZDg2NGJmN2EwNzAuYmluZFBvcHVwKHBvcHVwX2U0YTM0MzE1NTAwZTQ2MjE5YzRlNWNlYWUyYmIyNGM2KTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzNlODhhMDZmMzZjNzQwNWQ4MWE1OWI0ODZlNWU4NWEwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDY0MDgxNDczNDc2MjA2LDkuMTg4NTU4ODIzNjk3NjNdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMDJkZWQ1ODdhYmEzNDY1NzljODI1Mjg3NzE0ZmY0NTIgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfMzZkMjZkNzdhNDdhNDI4YzhkMjY3YTNhMTg0NTQxYWUgPSAkKCc8ZGl2IGlkPSJodG1sXzM2ZDI2ZDc3YTQ3YTQyOGM4ZDI2N2EzYTE4NDU0MWFlIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5JdGFsaWFuIFJlc3RhdXJhbnQ8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzAyZGVkNTg3YWJhMzQ2NTc5YzgyNTI4NzcxNGZmNDUyLnNldENvbnRlbnQoaHRtbF8zNmQyNmQ3N2E0N2E0MjhjOGQyNjdhM2ExODQ1NDFhZSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8zZTg4YTA2ZjM2Yzc0MDVkODFhNTliNDg2ZTVlODVhMC5iaW5kUG9wdXAocG9wdXBfMDJkZWQ1ODdhYmEzNDY1NzljODI1Mjg3NzE0ZmY0NTIpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYmVkNjEyMDA1ODhmNDFmNmE2OTkyOWY1ZTY0MDZhNDkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTIyMTIzMDY1MjE5OCw5LjE4MjkzODM4MzE1NDcyNF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9hODJiNWJkNDQ3ZDk0NjhkOWNlZjgxYmU2YmE5OTNlYyA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8xNDFiODM1ZDRiYjA0YjQ4OTc1Yjc3NTIxMDFkOGM3OCA9ICQoJzxkaXYgaWQ9Imh0bWxfMTQxYjgzNWQ0YmIwNGI0ODk3NWI3NzUyMTAxZDhjNzgiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNhZsOpPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9hODJiNWJkNDQ3ZDk0NjhkOWNlZjgxYmU2YmE5OTNlYy5zZXRDb250ZW50KGh0bWxfMTQxYjgzNWQ0YmIwNGI0ODk3NWI3NzUyMTAxZDhjNzgpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfYmVkNjEyMDA1ODhmNDFmNmE2OTkyOWY1ZTY0MDZhNDkuYmluZFBvcHVwKHBvcHVwX2E4MmI1YmQ0NDdkOTQ2OGQ5Y2VmODFiZTZiYTk5M2VjKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzEzNTM0OGI5YjY0NjRiYzQ4OGI5NTI5MjQ1ZTBhNDlmID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDUwNzI3LDkuMTgwMDk5XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzlmNWQzMjgxYWRjZTQ2NTY4MTdiOTVmYTAyNGY5NDI0ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzY2YTBlNGQwNDM2MjQzZDE5MzkwMjU4NDZmMTdlZDg4ID0gJCgnPGRpdiBpZD0iaHRtbF82NmEwZTRkMDQzNjI0M2QxOTM5MDI1ODQ2ZjE3ZWQ4OCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2Fmw6k8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzlmNWQzMjgxYWRjZTQ2NTY4MTdiOTVmYTAyNGY5NDI0LnNldENvbnRlbnQoaHRtbF82NmEwZTRkMDQzNjI0M2QxOTM5MDI1ODQ2ZjE3ZWQ4OCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8xMzUzNDhiOWI2NDY0YmM0ODhiOTUyOTI0NWUwYTQ5Zi5iaW5kUG9wdXAocG9wdXBfOWY1ZDMyODFhZGNlNDY1NjgxN2I5NWZhMDI0Zjk0MjQpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfODI3MmMwNTFkZmE4NDlhZjk2NzFiZWE5ZThlMDFkMGYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTEzNDI4OTMxODQ2NDUsOS4xNzc2ODcwMTY5Mjk5MThdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfZjAyMmFmOWJlNTEyNGYwNGIzNGIzZTZjMTQzODkzOTMgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNTkxN2JmYjc1YTY1NDNlNmIyNmVkZGNiNzIyMmUwYzEgPSAkKCc8ZGl2IGlkPSJodG1sXzU5MTdiZmI3NWE2NTQzZTZiMjZlZGRjYjcyMjJlMGMxIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DYWbDqTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZjAyMmFmOWJlNTEyNGYwNGIzNGIzZTZjMTQzODkzOTMuc2V0Q29udGVudChodG1sXzU5MTdiZmI3NWE2NTQzZTZiMjZlZGRjYjcyMjJlMGMxKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzgyNzJjMDUxZGZhODQ5YWY5NjcxYmVhOWU4ZTAxZDBmLmJpbmRQb3B1cChwb3B1cF9mMDIyYWY5YmU1MTI0ZjA0YjM0YjNlNmMxNDM4OTM5Myk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl82MDVlNmM1MmMwNWE0Zjk3ODZjYWZhYzNiNTJkMWZjMSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ1NDM1ODgzMDAxMTc0LDkuMTczODEzODAzNDEzODgyXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzgxNjUzYjA0NWI4MDQwODRiYWE0ZmY1MTFiYTA5NjE4ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzAzNjg5MmI1ZTI0NTRmODZiMzVhNGQyY2RjNDBkYzNjID0gJCgnPGRpdiBpZD0iaHRtbF8wMzY4OTJiNWUyNDU0Zjg2YjM1YTRkMmNkYzQwZGMzYyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UGl6emEgUGxhY2U8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzgxNjUzYjA0NWI4MDQwODRiYWE0ZmY1MTFiYTA5NjE4LnNldENvbnRlbnQoaHRtbF8wMzY4OTJiNWUyNDU0Zjg2YjM1YTRkMmNkYzQwZGMzYyk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl82MDVlNmM1MmMwNWE0Zjk3ODZjYWZhYzNiNTJkMWZjMS5iaW5kUG9wdXAocG9wdXBfODE2NTNiMDQ1YjgwNDA4NGJhYTRmZjUxMWJhMDk2MTgpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYzgwYTUxYjA3MzEyNDUyOWI4ZjJhODU0MzA2ODVkMDIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTM5MzU4ODU4MzAyLDkuMTk2MDcyNzg0NjI4OTAzXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzIyMzJiMWU5MmFiOTQzZjM5NjI2YWE1NjJhMDUyY2YwID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2QzNDgzZmI5NGM2MDQ1NjM5ODIzMTkwOTAxOGRiMGE4ID0gJCgnPGRpdiBpZD0iaHRtbF9kMzQ4M2ZiOTRjNjA0NTYzOTgyMzE5MDkwMThkYjBhOCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2Fmw6k8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzIyMzJiMWU5MmFiOTQzZjM5NjI2YWE1NjJhMDUyY2YwLnNldENvbnRlbnQoaHRtbF9kMzQ4M2ZiOTRjNjA0NTYzOTgyMzE5MDkwMThkYjBhOCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9jODBhNTFiMDczMTI0NTI5YjhmMmE4NTQzMDY4NWQwMi5iaW5kUG9wdXAocG9wdXBfMjIzMmIxZTkyYWI5NDNmMzk2MjZhYTU2MmEwNTJjZjApOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNWI1YjM5NGNhODVjNGJmMmI4ZDhhMGZmYjZjMTM5ZTkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTU0MzYyMDY1MzYwODUsOS4xNjgzMDc1MjQwNjA2ODVdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfOTIxY2IyYTkxNWViNGI1NjkyYjBlNDhlYjBlMzJjNDggPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNTFhYTNkYzg1OWI5NGI4OWI3YWYwNjcxNmE1YTNmNDUgPSAkKCc8ZGl2IGlkPSJodG1sXzUxYWEzZGM4NTliOTRiODliN2FmMDY3MTZhNWEzZjQ1IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5JdGFsaWFuIFJlc3RhdXJhbnQ8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzkyMWNiMmE5MTVlYjRiNTY5MmIwZTQ4ZWIwZTMyYzQ4LnNldENvbnRlbnQoaHRtbF81MWFhM2RjODU5Yjk0Yjg5YjdhZjA2NzE2YTVhM2Y0NSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl81YjViMzk0Y2E4NWM0YmYyYjhkOGEwZmZiNmMxMzllOS5iaW5kUG9wdXAocG9wdXBfOTIxY2IyYTkxNWViNGI1NjkyYjBlNDhlYjBlMzJjNDgpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNDdkZjhkMzhmMmJhNGY4Yzk3ZWM3MDM1ZDk1YjU0ZDEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NjY5MDQ3NTA1NDYxNiw5LjE4NTkzNDIxNTY5MDkxNF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF81Mzk0MTg5MTI1NDI0NzFjYjEwMWI4MzU5MjMzNmEzZiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF80NjMwNjNhYWVkYTc0OGE4YTk1YWQ1MmI1Y2FjMDJhMiA9ICQoJzxkaXYgaWQ9Imh0bWxfNDYzMDYzYWFlZGE3NDhhOGE5NWFkNTJiNWNhYzAyYTIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNhZsOpPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF81Mzk0MTg5MTI1NDI0NzFjYjEwMWI4MzU5MjMzNmEzZi5zZXRDb250ZW50KGh0bWxfNDYzMDYzYWFlZGE3NDhhOGE5NWFkNTJiNWNhYzAyYTIpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNDdkZjhkMzhmMmJhNGY4Yzk3ZWM3MDM1ZDk1YjU0ZDEuYmluZFBvcHVwKHBvcHVwXzUzOTQxODkxMjU0MjQ3MWNiMTAxYjgzNTkyMzM2YTNmKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2Q5NThiN2JlNGI1MTQ0MmY4Nzk4NWRmYWJhNzZjODY3ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDUwNDUxMTkyNTQ3MzUsOS4xNjM1NzAxOTcxMzk2NTddLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfYzAzYTBhMWNlNDNlNDM1MWEyZmNlNzZlMjA4MzUxYjggPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNDQyNmFkYTUzOTJjNGU3ZGEyNzJkNmU0YjY2NTFiMTUgPSAkKCc8ZGl2IGlkPSJodG1sXzQ0MjZhZGE1MzkyYzRlN2RhMjcyZDZlNGI2NjUxYjE1IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DYWbDqTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfYzAzYTBhMWNlNDNlNDM1MWEyZmNlNzZlMjA4MzUxYjguc2V0Q29udGVudChodG1sXzQ0MjZhZGE1MzkyYzRlN2RhMjcyZDZlNGI2NjUxYjE1KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2Q5NThiN2JlNGI1MTQ0MmY4Nzk4NWRmYWJhNzZjODY3LmJpbmRQb3B1cChwb3B1cF9jMDNhMGExY2U0M2U0MzUxYTJmY2U3NmUyMDgzNTFiOCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81M2FmYzg0ZWY4YjQ0NzUxOTNiNTVlOTZiNDRjY2JhNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ1MTkzMTk3NzI1MjQ4NSw5LjE4NDI1MDk2ODYwNDM5XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzkzNWZiM2ExOWE5YTRkMmI5NzQ2NzBmMGYyZWEyOGIzID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzlmMjA0MmI3OWVhYTRhZjA5OTNlMzE1YzI1ZTdkZGEwID0gJCgnPGRpdiBpZD0iaHRtbF85ZjIwNDJiNzllYWE0YWYwOTkzZTMxNWMyNWU3ZGRhMCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2Fmw6k8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzkzNWZiM2ExOWE5YTRkMmI5NzQ2NzBmMGYyZWEyOGIzLnNldENvbnRlbnQoaHRtbF85ZjIwNDJiNzllYWE0YWYwOTkzZTMxNWMyNWU3ZGRhMCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl81M2FmYzg0ZWY4YjQ0NzUxOTNiNTVlOTZiNDRjY2JhNi5iaW5kUG9wdXAocG9wdXBfOTM1ZmIzYTE5YTlhNGQyYjk3NDY3MGYwZjJlYTI4YjMpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfOWE4NTEzMzFlZGZjNGE2Yzg1NjIzMTgyZDg2NTI1OTIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTQyMjU3MTc0NDg4NjQsOS4xNzQwMDAwNjI3Mjk3NDZdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNDBmNTZlNGZkNTE0NDQ3YWEzZDZmMjhiNWEyYmYzZmIgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfOTJkOTE4ZTU3OGU1NDFjZTliY2Y4OTMzNDUxZmEwNTcgPSAkKCc8ZGl2IGlkPSJodG1sXzkyZDkxOGU1NzhlNTQxY2U5YmNmODkzMzQ1MWZhMDU3IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5QaXp6YSBQbGFjZTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfNDBmNTZlNGZkNTE0NDQ3YWEzZDZmMjhiNWEyYmYzZmIuc2V0Q29udGVudChodG1sXzkyZDkxOGU1NzhlNTQxY2U5YmNmODkzMzQ1MWZhMDU3KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzlhODUxMzMxZWRmYzRhNmM4NTYyMzE4MmQ4NjUyNTkyLmJpbmRQb3B1cChwb3B1cF80MGY1NmU0ZmQ1MTQ0NDdhYTNkNmYyOGI1YTJiZjNmYik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9mMTQxM2FjNTZiOTU0OTc1ODdmYjIyZGZhZWY5YzQwOSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ1MTc1MTYyMzkzNDYyLDkuMTc4MTgwNjU1MTk2NTU4XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzU4MTJiM2IyMWU3ZjQ4MDJhOTAzMmMwOTY1Yzg4MTU5ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2NkZjU0OGVkZGQ2MTQxYzI4NWYxZTVmOWI5YjUxMGNkID0gJCgnPGRpdiBpZD0iaHRtbF9jZGY1NDhlZGRkNjE0MWMyODVmMWU1ZjliOWI1MTBjZCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+T3RoZXIgTmlnaHRsaWZlPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF81ODEyYjNiMjFlN2Y0ODAyYTkwMzJjMDk2NWM4ODE1OS5zZXRDb250ZW50KGh0bWxfY2RmNTQ4ZWRkZDYxNDFjMjg1ZjFlNWY5YjliNTEwY2QpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfZjE0MTNhYzU2Yjk1NDk3NTg3ZmIyMmRmYWVmOWM0MDkuYmluZFBvcHVwKHBvcHVwXzU4MTJiM2IyMWU3ZjQ4MDJhOTAzMmMwOTY1Yzg4MTU5KTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzAyMDBlYzE0NGNkODQ2OWM4ZmUyMTcyNDBkZWFhMjZiID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDUyNDYzNDM3MjMxMDk2LDkuMTg0NzQ3MjM1MTk5NzE1XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzdlMjJjMTVhNzRhZTQ1ZDI5NjhlYjYyYTgxNjJjZTRiID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2VhMGIxZjEwZWU0NDQ3NjRiYmFkZDQwNDQ0ZGFmODhiID0gJCgnPGRpdiBpZD0iaHRtbF9lYTBiMWYxMGVlNDQ0NzY0YmJhZGQ0MDQ0NGRhZjg4YiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2Fmw6k8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzdlMjJjMTVhNzRhZTQ1ZDI5NjhlYjYyYTgxNjJjZTRiLnNldENvbnRlbnQoaHRtbF9lYTBiMWYxMGVlNDQ0NzY0YmJhZGQ0MDQ0NGRhZjg4Yik7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8wMjAwZWMxNDRjZDg0NjljOGZlMjE3MjQwZGVhYTI2Yi5iaW5kUG9wdXAocG9wdXBfN2UyMmMxNWE3NGFlNDVkMjk2OGViNjJhODE2MmNlNGIpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNDE3NmUxM2UyMjQ5NGFiMmJiY2VhNTc3OTM4YTI3NjMgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTU2NzY0NzgyMDg3Nyw5LjE4Mzg5Nzg3MjY2MDU3NV0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF82NWMyMTkyYjNiMWY0ZTMwYmYzZmFkYTI0YzkzZDRkYSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8xMjg4YzdmM2QyODg0OWY1YTQ5NTk3YmIzNDJkNmI4MCA9ICQoJzxkaXYgaWQ9Imh0bWxfMTI4OGM3ZjNkMjg4NDlmNWE0OTU5N2JiMzQyZDZiODAiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNhZsOpPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF82NWMyMTkyYjNiMWY0ZTMwYmYzZmFkYTI0YzkzZDRkYS5zZXRDb250ZW50KGh0bWxfMTI4OGM3ZjNkMjg4NDlmNWE0OTU5N2JiMzQyZDZiODApOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNDE3NmUxM2UyMjQ5NGFiMmJiY2VhNTc3OTM4YTI3NjMuYmluZFBvcHVwKHBvcHVwXzY1YzIxOTJiM2IxZjRlMzBiZjNmYWRhMjRjOTNkNGRhKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzNlOTFmYWRiOWI1NjQ2MDViZGM2MWQ2MzA5YzhmNmIwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDY0NTM1NDE4OTQ3OTc1LDkuMTkwMzUyMjU5MDM4NTIxXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2MyZjZmMzk3Nzc2NjRlNzU4ZWM3ODExM2YwY2JhZWQ1ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2Q4YWM1YjFjMWQ4MzQ3ODViNGFhNjViODQ1MDlkZWNkID0gJCgnPGRpdiBpZD0iaHRtbF9kOGFjNWIxYzFkODM0Nzg1YjRhYTY1Yjg0NTA5ZGVjZCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+SXRhbGlhbiBSZXN0YXVyYW50PC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9jMmY2ZjM5Nzc3NjY0ZTc1OGVjNzgxMTNmMGNiYWVkNS5zZXRDb250ZW50KGh0bWxfZDhhYzViMWMxZDgzNDc4NWI0YWE2NWI4NDUwOWRlY2QpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfM2U5MWZhZGI5YjU2NDYwNWJkYzYxZDYzMDljOGY2YjAuYmluZFBvcHVwKHBvcHVwX2MyZjZmMzk3Nzc2NjRlNzU4ZWM3ODExM2YwY2JhZWQ1KTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzM1YWQ3NjVjNmE1ZDQ2ZTNhNWY0MjhjNDVjNTZlYzFkID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDUuNDUxODUyNzgzMjIwNTMsOS4xODc3OTA1OTU3NDIzMzVdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfOWE3ZWZkZTI2OWVmNDBmZjgwMmViN2QzMGU4NTNmYmMgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNWJhMjgzZjY3N2U3NDMzNDgyODFjYTc0MjYyMjQ5MDkgPSAkKCc8ZGl2IGlkPSJodG1sXzViYTI4M2Y2NzdlNzQzMzQ4MjgxY2E3NDI2MjI0OTA5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5XaW5lIEJhcjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfOWE3ZWZkZTI2OWVmNDBmZjgwMmViN2QzMGU4NTNmYmMuc2V0Q29udGVudChodG1sXzViYTI4M2Y2NzdlNzQzMzQ4MjgxY2E3NDI2MjI0OTA5KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzM1YWQ3NjVjNmE1ZDQ2ZTNhNWY0MjhjNDVjNTZlYzFkLmJpbmRQb3B1cChwb3B1cF85YTdlZmRlMjY5ZWY0MGZmODAyZWI3ZDMwZTg1M2ZiYyk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl85ZjMwNTJmYzlhM2M0OTQ5YTE0ZTczNmJiMGYwYmJiOSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ0OTAxNTExMDMxMTc5LDkuMTc2NjczNDkxMjk2MzQxXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzRhNWM0NGRmOGZjNTQ3N2JiMjZkMjk1MjhlODExMmFlKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzRhNTc2ZDc2Mjc4ZTRiZWJiMzZjNzRlMTMwNjcyYTM3ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2U3ZGUxMjUwODVjMjQwYTZhMzlmMmMxMmQxNTUwYWNlID0gJCgnPGRpdiBpZD0iaHRtbF9lN2RlMTI1MDg1YzI0MGE2YTM5ZjJjMTJkMTU1MGFjZSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Rm9vZCAmIERyaW5rIFNob3A8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzRhNTc2ZDc2Mjc4ZTRiZWJiMzZjNzRlMTMwNjcyYTM3LnNldENvbnRlbnQoaHRtbF9lN2RlMTI1MDg1YzI0MGE2YTM5ZjJjMTJkMTU1MGFjZSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl85ZjMwNTJmYzlhM2M0OTQ5YTE0ZTczNmJiMGYwYmJiOS5iaW5kUG9wdXAocG9wdXBfNGE1NzZkNzYyNzhlNGJlYmIzNmM3NGUxMzA2NzJhMzcpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMDI5YTY0MTEzZTBiNGRkMTljMjRlODlmODA1MWViZWUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NTMxMTQsOS4xNzQ2OThdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfOWZkZTNkMDVmNWU1NDM5NGE0MjgxZWNhZDZkZjA1ZWMgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNzNkN2FlM2MwMTgyNDcxNjkzZjdmN2Y3YzZlNmIwZmYgPSAkKCc8ZGl2IGlkPSJodG1sXzczZDdhZTNjMDE4MjQ3MTY5M2Y3ZjdmN2M2ZTZiMGZmIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CYXI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzlmZGUzZDA1ZjVlNTQzOTRhNDI4MWVjYWQ2ZGYwNWVjLnNldENvbnRlbnQoaHRtbF83M2Q3YWUzYzAxODI0NzE2OTNmN2Y3ZjdjNmU2YjBmZik7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8wMjlhNjQxMTNlMGI0ZGQxOWMyNGU4OWY4MDUxZWJlZS5iaW5kUG9wdXAocG9wdXBfOWZkZTNkMDVmNWU1NDM5NGE0MjgxZWNhZDZkZjA1ZWMpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMTk0NWNhZDFiMzhiNGUzNjhhMWI5ZjVjMTljYTI4ZDkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0NS40NjMwMzE3NjQ2MDY3NTQsOS4xODg0MjM0OTUyMDY4NTldLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNGE1YzQ0ZGY4ZmM1NDc3YmIyNmQyOTUyOGU4MTEyYWUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfZGM5NmRmZTExNmJhNDg1Yzg3NDI5N2JmM2M0MmRjN2MgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfMjE1NzQ1NzllMWEyNGZmODg2MDVlN2Q3MTczMmUzNzQgPSAkKCc8ZGl2IGlkPSJodG1sXzIxNTc0NTc5ZTFhMjRmZjg4NjA1ZTdkNzE3MzJlMzc0IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DYWbDqTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZGM5NmRmZTExNmJhNDg1Yzg3NDI5N2JmM2M0MmRjN2Muc2V0Q29udGVudChodG1sXzIxNTc0NTc5ZTFhMjRmZjg4NjA1ZTdkNzE3MzJlMzc0KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzE5NDVjYWQxYjM4YjRlMzY4YTFiOWY1YzE5Y2EyOGQ5LmJpbmRQb3B1cChwb3B1cF9kYzk2ZGZlMTE2YmE0ODVjODc0Mjk3YmYzYzQyZGM3Yyk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8yNGM1MzliZmRjZDY0ZGQ0OTBlNzZiNTJkYzA5ZDY4ZSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQ1LjQ2MjQ3ODk5MDQ2NzM0Niw5LjE5MjYxNzMxMDAxMTg4OF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YTVjNDRkZjhmYzU0NzdiYjI2ZDI5NTI4ZTgxMTJhZSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF81MDM1MGI5ZjQ4Y2Q0ZDIxOTlkZGNhZGU3ZmU1YTVkOCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9jOWRiM2YyYzk4NjQ0MGJlOWZkOTgwN2FlYjdhNTFhZiA9ICQoJzxkaXYgaWQ9Imh0bWxfYzlkYjNmMmM5ODY0NDBiZTlmZDk4MDdhZWI3YTUxYWYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkFzaWFuIFJlc3RhdXJhbnQ8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzUwMzUwYjlmNDhjZDRkMjE5OWRkY2FkZTdmZTVhNWQ4LnNldENvbnRlbnQoaHRtbF9jOWRiM2YyYzk4NjQ0MGJlOWZkOTgwN2FlYjdhNTFhZik7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8yNGM1MzliZmRjZDY0ZGQ0OTBlNzZiNTJkYzA5ZDY4ZS5iaW5kUG9wdXAocG9wdXBfNTAzNTBiOWY0OGNkNGQyMTk5ZGRjYWRlN2ZlNWE1ZDgpOwoKICAgICAgICAgICAgCiAgICAgICAgCjwvc2NyaXB0Pg== onload="this.contentDocument.open();this.contentDocument.write(atob(this.getAttribute('data-html')));this.contentDocument.close();" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>




```python

```


```python

```
