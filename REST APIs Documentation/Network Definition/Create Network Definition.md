
# Create Network Definition API Design

## ***POST*** V1/network-definition
This API is used to create a Network Definition.

## Detail Information

> **Title** : Create Network Definition<br>

> **Version** : 28/01/2026

> **API Server URL** : http(s):// IP address of your NetBrain Web API Server/ServicesAPI/API/V1/network-definition

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
|devSubTypeName*|string| Device Type Name. |
|devDriverName*|string| Device Driver Name. |
|ipAddrRange*|string| IP Address Range. |
|isRegx^|bool| Default: `True` |


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
|success| bool | `True` - Success <br>`False` - Failure  |
|statusCode| int | The returned status code of executing the API.  |
|statusDescription| string | The explanation of the status code.  |

# Examples:
```python
full_url = nb_url + "/ServicesAPI/API/V1/network-definition"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"]=token

data = {
    "devSubTypeName": "Cisco Router",
    "devDriverName": "Cisco Router",
    "ipAddrRange": "192.168.32.100",
    "isRegx": False
}
try:
    response = requests.post(full_url, headers = headers, data = json.dumps(data), verify = False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Create Network Definition! - " + str(response.text))
    
except Exception as e:
    print (str(e)) 
```
```python
{'success': True, 'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman
```python
curl -X POST \
  http://192.168.28.44/ServicesAPI/API/V1/network-definition \
  -H "Content-Type: application/json"
  -H 'token: 1eff54e2-1df0-45eb-8382-67b668147deb' \
  -d '{
    "devSubTypeName": "Cisco Router",
    "devDriverName": "Cisco Router",
    "ipAddrRange": "192.168.32.100",
    "isRegx": false
}'
```
