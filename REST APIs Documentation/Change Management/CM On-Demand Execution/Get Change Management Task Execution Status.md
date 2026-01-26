
# Get Change Management Task Execution Status API Design

## ***GET*** /V3/CM/Status/{taskId}
Call this API to get the Change Management Task's Execution Status.

## Detail Information

> **Title** : Get Change Management Task Execution Status API<br>

> **Version** : 21/01/2026.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V3/CM/Status/{taskId}

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
|taskId*|string| Task ID. |

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
|taskStatus | int | 0 - Waiting <br>1 - Running<br> 2 - Stopped<br> 3 - Finished |
|executionStatus| array of objects | Execution Status. |
|executionStatus.nodeName| string | Node Name. |
|executionStatus.status| int |0 - Ready<br> 1 - Running<br> 2 - Approved<br> 3 - Completed<br> 4 - Locked<br> 5 - Executed |
|executionStatus.executionSummary| array of objects | Execution Summary in following field; `executed`, `changesSucceeded`, `changesFailed`, `rollbacksSucceeded`, `rollbacksFailed`<br> 0 - False<br> 1 - True<br>|
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

taskId = '1747ffb2-8acb-4aa5-9781-30b2d96f3375'
full_url = nb_url + f"/ServicesAPI/API/V3/CM/Status/{taskId}"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

try:
    response = requests.get(full_url, headers=headers, data = data, verify=False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Get Change Managament Execution Status! - " + str(response.text))
    
except Exception as e:
    print (str(e)) 
```
```python
{'taskStatus': 3, 'executionStatus': [{'nodeName': 'Execute', 'status': 5, 'executionSummary': {'executed': 1, 'changesSucceeded': 0, 'changesFailed': 1, 'rollbacksSucceeded': 0, 'rollbacksFailed': 0}}], 'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman

```python
curl -X GET \
  http://192.168.28.44/ServicesAPI/API/V3/CM/Status/1747ffb2-8acb-4aa5-9781-30b2d96f3375 \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H 'token: 2546a7e0-e041-495b-8ddb-23ef5eb15ff5' \
```
