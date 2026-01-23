
# Execute Change Management Task API Design

## ***POST*** /V3/CM/Execute
Call this API to execute the Network Change Management Task with nodes and functions involved in it.
<br>

## Detail Information

> **Title** : Execute Change Management Task API<br>

> **Version** : 21/01/2026.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V3/CM/Execute

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|||* - required<br />^ - optional|
|runbookId*|string| Runbook ID. |
|ttl-in-minutes^|int|Value must be > 1 <br> Default: `1 day`. |

> **Example**
```python
{
    "runbookId":"07cc24be-003f-4111-a1d7-d86430ffa586",
    "ttl-in-minutes":5
}
```

## Parameters(****required***)

> No required parameters.


## Headers

> **Data Format Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Content-Type | string  | support "application/json" |
| Accept | string | support "application/json" |

> **Authorization Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| token | string  | Authentication token, get from login API. |

## Response
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|taskId | string | Task ID. |
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

full_url = nb_url + "/ServicesAPI/API/V3/CM/Execute"

headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

runbookId = '4f4d3d45-a04d-407b-a4e7-ad6e1fd9f36f'

data = {
    "runbookId":runbookId,
     "ttl-in-minutes":5
}
try:
    response = requests.post(full_url, headers=headers, data = json.dumps(data), verify=False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Execute the Change Management Task! - " + str(response.text))
    
except Exception as e:
```
```python
{'taskId': '1747ffb2-8acb-4aa5-9781-30b2d96f3375', 'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman
```python
curl -X POST \
  http://192.168.28.44/ServicesAPI/API/V3/CM/Execute \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H 'token: 2546a7e0-e041-495b-8ddb-23ef5eb15ff5' \
  -d '{
    "runbookId":"b44728a0-7565-4587-b894-d0335d78a18d",
    "ttl-in-minutes":5
}'
```
