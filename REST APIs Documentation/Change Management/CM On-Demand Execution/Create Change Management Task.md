
# Create Change Management Task API Design

## ***POST*** /V3/CM
Call this API to create a Network Change Management Task with nodes and functions involved in it.
<br>

## Detail Information

> **Title** : Create Change Management Task API<br>

> **Version** : 21/01/2026.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V3/CM

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=1000/>|
|||* - required<br />^ - optional|
|name*|string| Change Management Task name. |
|runbookTemplate^|string| Change Management runbook template ID or Path. |
|mapPath^|string| Path to existing map, or where the new map will be created. <br> Default location: `Public/Network Changes/{cmname}/{timestamp}`|
|createIncident^|bool| Whether or not to create an incident for this Change Management Task. <br> Default: `False` |
|defineChangeNodes*|array of object| Settings for the `Define Change` nodes in the runbook. |
|defineChangeNodes.nodeName|string| Name of `Define Change` node of the runbook. <br> Default: Name of the first `Define Change` node. |
|defineChangeNodes.configlet^|array| The network change script. |
|defineChangeNodesconfigletTemplate^|array| The script <b>template name</b> for network change. <br>Only applies if the `configlet` field is empty. |
|defineChangeNodes.rollback^|array| The rollback script. |
|defineChangeNodes.rollbackTemplate^|array| The script <b>template name</b> for rollback script. <br>Only applies if the `rollback` field is empty|
|defineChangeNodes.devices*|array| Array of device name. <br> If no devices exists, the CM creation will fail. <br>e.g. `['dev1', 'dev2]` |
|templateVars^|string| Only applies for  Change Management created from a <b>template-based</b> runbook template. |
||||
|templateVars.singleVars|array of object| For instantiation of the single template variables. |
|templateVars.singleVars.name|template variable name| It is imperative the user knows the exact name by opening a runbook template on NetBrain UI. <br>The <b>name</b> specified in the API must match the name on UI. <br>`_TargetDevices` is a built-in variable name.|
|templateVars.singleVars.values|array of string| Template Value.|
||||
|templateVars.singleVars|array of object| For instantiation of the table template variables. |
|templateVars.singleVars.tableName|template variable name| Variable name of the table variable.|
|templateVars.singleVars.columns|array of string| <br><table><tr><th>Name</th><th>Type</th><th>Description</th></tr> <tr><td>name</td><td>Column name</td><td>User must check the actual column name on UI</td></tr> <tr><td>type</td><td>One of the following:<br>string, int, float, bool, device, interface</td><td>User must check the actual column type on UI</td></tr> <tr><td>values</td><td>array of string</td><td> </td></tr> <tr></table>|

> **Example of `templateVars`**
```python
"templateVars":{
   "singleVars":[
   {
      "name":"_TargetDevices",
      "values":["US-R1"]
   },
   {
      "name":"singlevar1",
      "values":["a","b"]
   },
   {
      "name":"singlevar2",
      "values":["c","d"]
   }
 ]
}
```
```python
"templateVars":{
  "tableVars":[
  {
    "tableName":"tableVar",
    "columns":[
    {
      "name":"col1",
      "type":"string1",
      "values":["stringvar"]
     },
     {
       "name":"col2",
       "type":"int",
       "values":["2"]
     },
     {
        "name":"col3",
        "type":"bool",
        "values":["false"]
      },
      {
         "name":"col4",
         "type":"device",
         "values":["US-R1"]
      },
      {
         "name":"col5",
         "type":"float",
         "values":["1.1"]
      },
      {
         "name":"col6",
         "type":"interface",
         "values":["US-R1.intf1"]
       }
     ]
   }
 ]
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
|runbookId | string | Runbook ID. |
|runbookUrl| string | Runbook URL. |
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

full_url = nb_url + "/ServicesAPI/API/V3/CM"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

data={
    "name": "API_TEST_CHANGE_TASK",
    "runbookTemplate": "",
    "mapPath": "",
    "createIncident": True,
    "defineChangeNodes": [
        {
            "nodeName": "",
            "configlet": "conf t\n interface GigabitEthernet0/46\n shutdown\n no shutdown",
            "configletTemplate": "conf t\\n interface e0/0\\n shutdown",
            "rollback": "conf t\n  GigabitEthernet0/46\n no shutdown",
            "rollbackTemplate": "",
            "devices": [
                "ASA"
            ]
        }
    ],
    "templateVars": {
        "singleVars": [],
        "tableVars": []
    }
}

try:
    response = requests.post(full_url, headers=headers, data = json.dumps(data), verify=False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Create a Change Management Task! - " + str(response.text))
    
except Exception as e:
    print (str(e)) 
```
```python
{'runbookId': 'cc87ff73-86eb-4078-bdc0-026c732c8ce2', 'runbookUrl': 'http://192.168.28.44/map.html?t=4cab3cc8-81e7-f4ce-ce1d-df056e9eff8e&d=535743d1-a4c6-47ad-aeee-327ba7950243&id=392102fe-55f0-4f5d-9649-6a2967c94cca&rba=cc87ff73-86eb-4078-bdc0-026c732c8ce2', 'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman

```python
curl -X POST \
  http://192.168.28.44/ServicesAPI/API/V3/CM \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H 'token: 0708493d-cc78-43a4-817e-6617b0777d3c' \
  -d '{
    "name": "API_TEST_CHANGE_TASK",
    "runbookTemplate": "",
    "mapPath": "",
    "createIncident": true,
    "defineChangeNodes": [
      {
        "nodeName": "",
        "configlet": "conf t\n interface GigabitEthernet0/46\n shutdown\n no shutdown",
        "configletTemplate": "conf t\n interface e0/0\n shutdown",
        "rollback": "conf t\n  GigabitEthernet0/46\n no shutdown",
        "rollbackTemplate": "",
        "devices": [
          "ASA"
        ]
      }
    ],
    "templateVars": {
      "singleVars": [],
      "tableVars": []
    }
  }'
```
