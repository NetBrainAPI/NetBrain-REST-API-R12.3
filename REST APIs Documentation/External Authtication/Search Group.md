
# External Authentication API Design

## ***POST*** /V1/CMDB/ExternalAuthtication/SearchGroup
Call this API to Search Group in NetBrain System Management.

## Detail Information

> **Title** : Search Group API<br>

> **Version** : 29/01/2026.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/ExternalAuthtication/SearchGroup

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|type* | int |  |
|pageIndex* | int |  |
|keyword | string |   |
|businessObj | object |  |
|businessObj.address* | string |   |
|businessObj.group_root | string | |
|businessObj.user_root | string ||
|businessObj.connectType | int ||
|businessObj.port|int||
|businessObj.connectName|string||
|businessObj.connectPwd|string||

## Parameters(****required***)

>No parameters required.

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
| token | string  | Authentication token, get from Login API. |

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|group|object||
|group.content.name|string|Name of the group|
|group.content.paths|string|Path of the group|
|group.content.systemRoles|list|System Roles of the group|
|group.content.portalOnly|bool||
|group.total|int|Total number of groups|
|group.needMore|bool|Indicates whether there are more groups|
|group.overLimit|bool||
|statusCode| int | The returned status code of executing the API.  |
|statusDescription| string | The explanation of the status code.  |

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
full_url = nb_url + "/ServicesAPI/API/V1/CMDB/ExternalAuthtication/SearchGroup"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

data = {
  "type": 2,
  "pageIndex": 1,
  "keyword": "",
  "businessObj": {
    "address": "192.168.31.168/dc=maxcrc,dc=com",
    "group_root": "",
    "user_root": "",
    "connectType": 0,
    "port": 389,
    "connectName": "cn=Manager,dc=maxcrc,dc=com",
    "connectPwd":"netbrain"
  }
}

try:
    response = requests.post(full_url, headers=headers, data = json.dumps(data), verify=False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Search Group! - " + str(response.text))
    
except Exception as e:
    print (str(e))  

```
```python
{
  "group": {
    "content": [
      {
        "name": "QAGroup",
        "path": "cn=QAGroup,ou=People,dc=maxcrc,dc=com",
        "systemRoles": [],
        "portalOnly": false
      },
      {
        "name": "testGroup1",
        "path": "cn=testGroup1,ou=People,dc=maxcrc,dc=com",
        "systemRoles": [],
        "portalOnly": false
      }
    ],
    "total": 2,
    "needMore": false,
    "overLimit": false
  },
  "statusCode": 790200,
  "statusDescription": "Success."
}
```

# cURL Code from Postman:
```python
curl -X POST \
  "http://192.168.28.44/ServicesAPI/API/V1/CMDB/ExternalAuthtication/SearchGroup" \
  -H "Content-Type: application/json" \
  -H "cache-control: no-cache" \
  -H "token: e798fe18-eb94-4b2e-87dc-31ba6b332f93" \
  -d '{ 
  "type": 2,
  "pageIndex": 1,
  "keyword": "",
  "businessObj": {
    "address": "192.168.31.168/dc=maxcrc,dc=com",
    "group_root": "",
    "user_root": "",
    "connectType": 0,
    "port": 389,
    "connectName": "cn=Manager,dc=maxcrc,dc=com",
    "connectPwd":"netbrain"
  }
}'
```

