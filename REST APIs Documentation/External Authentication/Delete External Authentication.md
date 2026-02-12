
# External Authentication API Design

## ***DELETE*** /V1/CMDB/ExternalAuthtication{?alias}
Call this API to delete External Authentication in NetBrain System Management.<br>
This API supports AD, and LDAP Authentications.

## Detail Information

> **Title** : Delete External Authentication API<br>

> **Version** : 29/01/2026.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/ExternalAuthtication{?alias}

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)
>No parameters required.

## Query Parameters(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|alias* | string | Name of the External Authentication |

## Headers

> **Data Format Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Content-Type | string | support "application/json" |
| Accept | string | support "application/json" |

> **Authorization Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| token | string  | Authentication token, get from Login API. |

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|statusCode| int | The returned status code of executing the API. |
|statusDescription| string | The explanation of the status code. |

# Full Example:
```python
# import python modules 
import requests
import time
import urllib3
import pprint
import json
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

token = "005fd6cc-cf08-4742-985b-902503dad2a4"
full_url = nb_url + "/ServicesAPI/API/V1/CMDB/ExternalAuthtication?alias=192.168.31.168"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

try:
    response = requests.delete(full_url, headers=headers, verify=False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Delete External LDAP Authentication! - " + str(response.text))
    
except Exception as e:
    print (str(e))  

```
```python
{'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman:
```python
curl -X DELETE \
  "http://192.168.28.44/ServicesAPI/API/V1/CMDB/ExternalAuthtication?alias=192.168.31.8" \
  -H "Content-Type: application/json" \
  -H "cache-control: no-cache" \
  -H "token: e798fe18-eb94-4b2e-87dc-31ba6b332f93"
```

