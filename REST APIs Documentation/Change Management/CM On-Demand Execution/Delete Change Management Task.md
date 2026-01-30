
# Delete Change Management Task API Design

## ***DELETE*** /V3/CM/{runbookId}
Call this API to delete the Network Change Management Task.
<br>

## Detail Information

> **Title** : Delete Change Management Task API<br>

> **Version** : 21/01/2026.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V3/CM/{runbookId}

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)
> No required parameters.

## Path Parameters(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|||* - required<br />^ - optional|
|runbookId*|string| Runbook ID. |


## Headers

> **Data Format Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Content-Type | string  | support "application/json" |
| Accept | string  | support "application/json" |

> **Authorization Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| token | string  | Authentication token, get from login API. |

## Response
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|statusCode| int | The returned status code of executing the API. |
|statusDescription| string | The explanation of the status code. |

# Full Example
```python
import requests
import time
import urllib3
import pprint
import json
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

token = "fd8b3f95-adc6-406d-9c18-bdb155de2ced"
runbookId = '67210d2f-808b-4f1a-b9eb-3a180f214777'

full_url = f"{nb_url}/ServicesAPI/API/V3/CM/{runbookId}"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

try:
    response = requests.delete(full_url, headers=headers, verify=False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Delete Change Management Task! - " + str(response.text))
    
except Exception as e:
    print (str(e))
```
```python
{'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman

```python
curl -X DELETE \
  http://192.168.28.44/ServicesAPI/API/V3/CM/67210d2f-808b-4f1a-b9eb-3a180f214777 \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H 'token: e2c80b1d-708d-4db4-8004-a8ab1bb8ad5c' \
```
