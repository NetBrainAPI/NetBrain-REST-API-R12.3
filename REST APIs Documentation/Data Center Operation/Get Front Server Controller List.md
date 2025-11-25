
# Get Front Server Controller List API Design

## ***GET*** /V1/CMDB/fsc/list
Call this API to get the list of Front Server Controller, including their base information and connected status.
<br>
As retrieving the connection status of FSC requires starting of the Worker Server, this API may be time-consuming.

## Detail Information

> **Title** : Get Front Server Controller List API<br>

> **Version** : 25/11/2025.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/fsc/list

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
As retrieving the connection status of FSC requires starting of the Worker Server, this API may be time-consuming.

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|name | string | The name of the FSC. |
|groupName| string | FSC Group Name. <br>Deploymet model is 1 - the value is FSC's uniqueName. <br>Deployment model is 2 - the value is the name of FSC Group  |
|ip| string | IP of FSC. |
|port| integer | Port of FSC. |
|timeout| DateTime | Timeout of FSC. |
|desc| string | Description of FSC. |
tenantInfo| object | Tenant Info. |
|tenantInfo.id| string | ID of the Tenant. |
|tenantInfo.name| string | Name of the Tenant. |
|connected| bool | The connected status of FSC. |
|statusCode| integer | The returned status code of executing the API. |
|statusDescription| string | The explanation of the status code. |

> ***Example***


```python
{
    "items": [
        {
            "name": "FSC",
            "groupName": "FSC",
            "ip": "10.99.98.1",
            "port": 9095,
            "timeout": 5,
            "tenants": [
                {
                    "id": "5aaad7c5-0a9b-44bd-b0e8-e6312c27a8b0",
                    "name": "Tenant1"
                },
                {
                    "id": "24201bff-b5c7-4810-94d9-3a908884bc35",
                    "name": "Tenant2"
                }
            ],
            "desc": "rrrr",
            "connected": true
        },
        {
            "name": "FSC1",
            "groupName": "Group1",
            "ip": "10.10.10.100",
            "port": 9095,
            "timeout": 5,
            "tenants": [],
            "desc": "",
            "connected": false
        },
        {
            "name": "FSC2",
            "groupName": "Group1",
            "ip": "10.10.10.1",
            "port": 9095,
            "timeout": 5,
            "tenants": [],
            "desc": "",
            "connected": false
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
full_url= nb_url + "/ServicesAPI/API/V1/CMDB/fsc/list"
    
try:
    # Do the HTTP request
    response = requests.get(full_url, headers=headers, verify=False)
    # Check for HTTP codes other than 200
    if response.status_code == 200:
        # Decode the JSON response into a dictionary and use the data
        result = response.json()
        print (result)
    else:
        print ("Failed to Get FSC List! - " + str(response.text))
    
except Exception as e:
    print (str(e)) 
```
```python
{'items': [{'name': 'FSC', 'groupName': 'FSC', 'ip': 'netbrain-nlb.netbrain.com', 'port': 9096, 'timeout': 5, 'tenants': [{'id': '131c38b8-9518-4118-8dd1-1ff27b7e38a9', 'name': 'NBLIVE-Sessions'}], 'desc': '', 'connected': True}], 'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman


```python
curl -X GET \
  https://nblive2025.netbrain.com/ServicesAPI/API/V1/CMDB/fsc/list \
  -H 'token: 8c7cc79a-040e-41c4-aec3-a6081bd7294a' \
  -H 'cache-control: no-cache' \
  -H 'token: fd8b3f95-adc6-406d-9c18-bdb155de2ced'
```
