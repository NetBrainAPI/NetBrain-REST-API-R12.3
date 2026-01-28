
# Get Network Definition API Design

## ***GET*** V1/network-definition
This API is used to retrieve the existing Network Definition.

## Detail Information

> **Title** : Get Network Definition<br>

> **Version** : 28/01/2026

> **API Server URL** : http(s):// IP address of your NetBrain Web API Server/ServicesAPI/API/V1/network-definition

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token |

## Request body(****required***)
>No parameters required.


## Parameters(****required***)
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|||* - required<br />^ - optional|
|pageIndex^|int| Page index <br>Default: `1` |
|pageSize^|int| Page size <br>Default: `100` |

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
|networkDefinitions| object | List of Network Definitions. |
|networkDefinitions.ID| string | ID of a Network Definition. |
|networkDefinitions.devNameExp| string |  |
|networkDefinitions.isRegx| bool |  |
|networkDefinitions.ipAddrRange| string | IP Address Range. |
|networkDefinitions.driverId| string | Driver ID of the associated Network Defintion. |
|networkDefinitions.devSubType| string |  |
|networkDefinitions.devDriverName| string | Driver Name. |
|networkDefinitions.devSubTypeName| string | Driver Device Type Name. |
|hasMore|bool|`True` - indicates there are more (there is next page)<br>`False` - indicates the end of the list.|
|statusCode| int | The returned status code of executing the API.  |
|statusDescription| string | The explanation of the status code.  |

# Examples:
```python
full_url = nb_url + "/ServicesAPI/API/V1/network-definition"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}

headers["Token"]=token

params = {
    "pageIndex": 1,
    "pageSize": 10
}

try:
    response = requests.get(full_url, headers=headers, params=params, verify=False)
    if response.status_code == 200:
        result = response.json()
        print(result)
    else:
        print("Failed to Get Network Definition! - " + response.text)
except Exception as e:
    print(str(e))
```
```python
{'networkDefinitions': [{'ID': 'ae548706-6c0b-8d91-e903-1f6354fffae5', 'devNameExp': None, 'isRegx': True, 'ipAddrRange': '192.168.0.40', 'driverId': '968644de-5d06-4fbc-9f80-97fc3f196420', 'devSubType': 2009, 'devDriverName': 'Cisco ASA Firewall', 'devSubTypeName': 'Cisco ASA Firewall'}, {'ID': 'bf94645f-e0a6-486a-84da-3cb633416370', 'devNameExp': None, 'isRegx': False, 'ipAddrRange': '172.24.31.0', 'driverId': 'b2d313fe-43e6-4d5f-9189-b3af6b71a83a', 'devSubType': 2, 'devDriverName': 'Cisco Router', 'devSubTypeName': 'Cisco Router'}], 'hasMore': False, 'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman
```python
curl -X GET  \
  http://192.168.28.44/ServicesAPI/API/V1/network-definition \
  -H "Content-Type: application/json"
  -H 'token: 1eff54e2-1df0-45eb-8382-67b668147deb' \
  -d '{
    "pageIndex": 1,
    "pageSize": 10
}'
```
