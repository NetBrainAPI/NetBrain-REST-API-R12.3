
# External Authentication API Design

## ***GET*** /V1/CMDB/ExternalAuthtication{?alias}
Call this API to get External Authentication in NetBrain System Management.

## Detail Information

> **Title** : Get External Authentication API<br>

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
|alias* | string |  |

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
|externalAuth|object|External object information|
|externalAuth.businessObj|object|External business object|
|bexternalAuth.businessObj.address|string|External Server Address|
|externalAuth.businessObj.group_root|string|Organizational Unit (OU) that the target user groups are located in. <br>e.g. `ou=G1`|
|externalAuth.businessObj.user_root|string|Organizational Unit (OU) where the target user accounts are located in. <br>e.g. `ou=G1`|
|externalAuth.businessObj.connectType|int|0 - Regular <br>1 - SSL|
|externalAuth.businessObj.port|int|External Server Port|
|externalAuth.businessObj.connectName|string| Username to connect to the server. <br><br>It is highly recommended to use the domain name/username format in the Connect Username fiel to avoid unexpected problems. <br>e.g. `test/administrator` <br><br> When more than 500 user groups are managed on LDAP server, the username used to connect to the server must be the <b>Manager</b>.<br> e.g. `CN=Manager,dc=test,dc=com`.|
|externalAuth.businessObj.groups|array of objects|Selected Group Info|
|externalAuth.businessObj.attributeMappings|array of objects|Mapping Attribute|
|externalAuth.id|string|External Authentication ID|
|externalAuth.alias|string|External Authentication Name|
|externalAuth.desc|string|External Authentication Description|
|externalAuth.type|int|External Authentication Type<br>`1` - AD<br>`2` - LDAP <br>`3` - TACACS <br>`4` - SAML|
|externalAuth.enabled|bool|Indicates to enable or disable External Authentication|
|externalAuth.displayServerName|string|External Server Address Information|
|externalAuth.needUpdated|bool|External Authentication Upgrade|
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
    response = requests.get(full_url, headers = headers, verify = False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Get External LDAP Authentication! - " + str(response.text))
    
except Exception as e:
    print (str(e))  

```
```python
{'externalAuth': {'businessObj': {'address': '192.168.31.8/dc=maxcrc,dc=com', 'group_root': '', 'user_root': '', 'connectType': 0, 'port': 389, 'connectName': 'cn=Manager,dc=maxcrc,dc=com', 'groups': [{'id': 'g_0a258155-0f27-436e-860f-b3f489745003', 'groupName': 'QAGroup', 'name': 'QAGroup', 'path': 'cn=QAGroup,ou=People,dc=maxcrc,dc=com', 'systemRoles': ['systemAdmin'], 'portalOnly': False, 'tenants': [{'id': '5aaad7c5-0a9b-44bd-b0e8-e6312c27a8b0', 'roles': ['tenantUser', 'tenantAdmin', 'addDomain'], 'domains': [{'guid': 'ba40a4fd-fd4d-4e40-bcb7-6111174b0488', 'roles': ['domainAdmin'], 'devicePolicies': []}, {'guid': '0c1f3ac0-7ba8-45be-90a8-14fc4ac801dd', 'roles': ['domainAdmin'], 'devicePolicies': []}]}]}, {'id': 'g_22831966-6ea6-43f6-9915-bfc25b326aaf', 'groupName': 'testGroup1', 'name': 'testGroup1', 'path': 'cn=testGroup1,ou=People,dc=maxcrc,dc=com', 'systemRoles': [], 'portalOnly': True, 'tenants': [{'id': '5aaad7c5-0a9b-44bd-b0e8-e6312c27a8b0', 'roles': ['tenantUser'], 'domains': [{'guid': 'ba40a4fd-fd4d-4e40-bcb7-6111174b0488', 'roles': [], 'devicePolicies': []}, {'guid': '0c1f3ac0-7ba8-45be-90a8-14fc4ac801dd', 'roles': [], 'devicePolicies': []}]}]}], 'attributeMappings': [{'enable': True, 'name': 'Username', 'mappingAttribute': 'uid;samaccountname'}, {'enable': True, 'name': 'First Name', 'mappingAttribute': 'givenName'}, {'enable': True, 'name': 'Last Name', 'mappingAttribute': 'sn'}, {'enable': True, 'name': 'Email', 'mappingAttribute': 'mail'}, {'enable': True, 'name': 'Description', 'mappingAttribute': 'description'}, {'enable': True, 'name': 'Phone Number', 'mappingAttribute': 'homePhone'}]}, 'id': 'b144d33d-455f-41c0-8fcb-54f0def583d0', 'alias': '192.168.31.168', 'desc': '', 'type': 2, 'enabled': True, 'displayServerName': '192.168.31.8/dc=maxcrc,dc=com', 'needUpdated': False}, 'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman:
```python
curl -X GET \
  "http://192.168.28.44/ServicesAPI/API/V1/CMDB/ExternalAuthtication?alias=192.168.31.8" \
  -H "Content-Type: application/json" \
  -H "cache-control: no-cache" \
  -H "token: e798fe18-eb94-4b2e-87dc-31ba6b332f93"
```

