
# Get Front Server List API Design

## ***GET*** /V1/CMDB/fs/list
Call this API to get the list of Front Server, including their base information and connected status.
<br>
As retrieving the connection status of FS requires starting of the Worker Server, this API may be time-consuming.

## Detail Information

> **Title** : Get Front Server List API<br>

> **Version** : 25/11/2025.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/fs/list

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)

>No request body.

## Parameters(****required***)

> No required parameters.


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
As retrieving the connection status of FS requires starting of the Worker Server, this API may be time-consuming.

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|id | string | ID of the FS. |
|ip| string | IP of FS. |
|alias| string | Hostname of FS. |
|registered| bool | Checks whether the FS is registered. |
|registeredTime| DateTime | Registration Time of FS. |
tenantInfo| object | Tenant Info. |
|tenantInfo.id| string | ID of the Tenant. |
|tenantInfo.name| string | Name of the Tenant. |
|connected| bool | The connected status of FS. |
|statusCode| integer | The returned status code of executing the API. |
|statusDescription| string | The explanation of the status code. |

> ***Example***


```python

{
    "items": [
        {
            "id": "FS1",
            "ip": "10.99.98.12",
            "alias": "CAN-DTP-090",
            "registered": true,
            "registeredTime": "2025-10-10T18:11:20Z",
            "tenantInfo": {
                "id": "5aaad7c5-0a9b-44bd-b0e8-e6312c27a8b0",
                "name": "Tenant1"
            },
            "connected": true
        }
    ],
    "statusCode": 790200,
    "statusDescription": "Success."
}
```
# Full Example
```python
import requests
import time
import urllib3
import pprint
import json
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

token = "fd8b3f95-adc6-406d-9c18-bdb155de2ced"

headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"]=token
full_url= nb_url + "/ServicesAPI/API/V1/CMDB/fs/list"
    
try:
    # Do the HTTP request
    response = requests.get(full_url, headers=headers, verify=False)
    # Check for HTTP codes other than 200
    if response.status_code == 200:
        # Decode the JSON response into a dictionary and use the data
        result = response.json()
        print (result)
    else:
        print ("Failed to Get FS List! - " + str(response.text))
    
except Exception as e:
    print (str(e)) 
```
```python
{'items': [{'id': 'FS_Hybrid', 'ip': '192.168.29.126', 'alias': 'BURWLABP0007', 'registered': True, 'registeredTime': '2025-11-24T22:40:29Z', 'tenantInfo': {'id': '131c38b8-9518-4118-8dd1-1ff27b7e38a9', 'name': 'Initial_Tenant'}, 'connected': True}], 'statusCode': 790200, 'statusDescription': 'Success.'}

```

# cURL Code from Postman


```python
curl -X GET \
  https://nblive2025.netbrain.com/ServicesAPI/API/V1/CMDB/fs/list \
  -H 'token: 8c7cc79a-040e-41c4-aec3-a6081bd7294a' \
  -H 'cache-control: no-cache' \
  -H 'token: fd8b3f95-adc6-406d-9c18-bdb155de2ced'
```
