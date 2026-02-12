
# External Authentication API Design

## ***POST*** /V1/CMDB/ExternalAuthtication/SaveExternalAuth
Call this API to save the External Authentication in NetBrain System Management.<br>
This API supports AD, and LDAP Authentications.

## Detail Information

> **Title** : Save External Authentication API<br>

> **Version** : 29/01/2026.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/ExternalAuthtication/SaveExternalAuth

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|businessObj* | object | External Object Information |
|address* | string | External Server Address |
|group_root^ | string | Group Root |
|user_root^ | string | User Root |
|connectType* | int | 0 - Regular <br>1 - SSL |
|port* | int |External Server Port |
|connectName* | string | Connect Username |
|groups* | array of object |Selected Group Info|
|isSystemAdmin*|bool|Indicates whether the user is a System Admin.|
|isSystemManager*|bool|Indicates whether the user is a System Manager.|
|isUserManager*|bool|Indicates whether the user is a User Manager.|

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
|statusCode| integer | The returned status code of executing the API.  |
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
full_url = nb_url + "/ServicesAPI/API/V1/CMDB/ExternalAuthtication/SaveExternalAuth"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

data = {
  "businessObj": {
    "address": "192.168.31.16/dc=maxcrc,dc=com",
    "group_root": "",
    "user_root": "",
    "connectType": 0,
    "port": 389,
    "connectName": "cn=Manager,dc=maxcrc,dc=com",
    "groups": [
      {
        "id": "g_0a258155-0f27-436e-860f-b3f489745003",
        "groupName": "QAGroup",
        "name": "QAGroup",
        "path": "cn=QAGroup,ou=People,dc=maxcrc,dc=com",
        "systemRoles": [
          "systemAdmin"
        ],
        "portalOnly": False,
        "tenants": [
          {
            "id": "5aaad7c5-0a9b-44bd-b0e8-e6312c28b0",
            "roles": [
              "tenantUser",
              "tenantAdmin",
              "addDomain"
            ],
            "domains": [
              {
                "guid": "ba40a4fd-fd4d-4e40-bcb7-61174b0488",
                "roles": [
                  "domainAdmin"
                ],
                "devicePolicies": []
              },
              {
                "guid": "0c1f3ac0-7ba8-45be-90a8-14fc4ac801dd",
                "roles": [
                  "domainAdmin"
                ],
                "devicePolicies": []
              }
            ]
          }
        ],
        "isSystemAdmin": True,
        "isSystemManager": False,
        "isUserManager": False
      },
      {
        "id": "g_2281966-6ea6-43f6-9915-bfc25326aaf",
        "groupName": "testGroup1",
        "name": "testGroup1",
        "path": "cn=testGroup1,ou=People,dc=maxcrc,dc=com",
        "systemRoles": [],
        "portalOnly": True,
        "tenants": [
          {
            "id": "5aaad7c5-0a9b-44bd-b0e8-e6312c27a8b0",
            "roles": [
              "tenantUser"
            ],
            "domains": [
              {
                "guid": "ba40a4fd-fd4d-4e40-bcb7-6111174b0488",
                "roles": [],
                "devicePolicies": []
              },
              {
                "guid": "0c1f3ac0-7ba8-45be-90a8-14fc4ac801dd",
                "roles": [],
                "devicePolicies": []
              }
            ]
          }
        ]
      }
    ],
    "attributeMappings": [
      {
        "enable": True,
        "name": "Username",
        "mappingAttribute": "uid;samaccountname"
      },
      {
        "enable": True,
        "name": "First Name",
        "mappingAttribute": "givenName"
      },
      {
        "enable": True,
        "name": "Last Name",
        "mappingAttribute": "sn"
      },
      {
        "enable": True,
        "name": "Email",
        "mappingAttribute": "mail"
      },
      {
        "enable": True,
        "name": "Description",
        "mappingAttribute": "description"
      },
      {
        "enable": True,
        "name": "Phone Number",
        "mappingAttribute": "homePhone"
      }
    ],
    "advancedSettings": ""
  },
  "id": "b144d33d-455f-41c0-8fcb-54f0def583d0",
  "alias": "192.168.31.168",
  "desc": "",
  "type": 2,
  "enabled": True,
  "testUserName": "xxxx@netbraintech.com",
  "testPassword": "Netbrain1123"
}

try:
    response = requests.post(full_url, headers=headers, data = json.dumps(data), verify=False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Failed to Save External LDAP Authentication! - " + str(response.text))
    
except Exception as e:
    print (str(e))  
```
```python
{'statusCode': 790200, 'statusDescription': 'Success.'}
```

# cURL Code from Postman:


```python
curl -X POST \
  "http://192.168.28.44/ServicesAPI/API/V1/CMDB/ExternalAuthtication/SaveExternalAuth" \
  -H "Content-Type: application/json" \
  -H "cache-control: no-cache" \
  -H "token: e798fe18-eb94-4b2e-87dc-31ba6b332f93" \
  -d '{
    "businessObj": {
      "address": "192.168.31.8/dc=maxcrc,dc=com",
      "group_root": "",
      "user_root": "",
      "connectType": 0,
      "port": 389,
      "connectName": "cn=Manager,dc=maxcrc,dc=com",
      "groups": [
        {
          "id": "g_0a258155-0f27-436e-860f-b3f489745003",
          "groupName": "QAGroup",
          "name": "QAGroup",
          "path": "cn=QAGroup,ou=People,dc=maxcrc,dc=com",
          "systemRoles": ["systemAdmin"],
          "portalOnly": false,
          "tenants": [
            {
              "id": "5aaad7c5-0a9b-44bd-b0e8-e6312c27a8b0",
              "roles": ["tenantUser","tenantAdmin","addDomain"],
              "domains": [
                {
                  "guid": "ba40a4fd-fd4d-4e40-bcb7-6111174b0488",
                  "roles": ["domainAdmin"],
                  "devicePolicies": []
                },
                {
                  "guid": "0c1f3ac0-7ba8-45be-90a8-14fc4ac801dd",
                  "roles": ["domainAdmin"],
                  "devicePolicies": []
                }
              ]
            }
          ],
          "isSystemAdmin": true,
          "isSystemManager": false,
          "isUserManager": false
        },
        {
          "id": "g_22831966-6ea6-43f6-9915-bfc25b326aaf",
          "groupName": "testGroup1",
          "name": "testGroup1",
          "path": "cn=testGroup1,ou=People,dc=maxcrc,dc=com",
          "systemRoles": [],
          "portalOnly": true,
          "tenants": [
            {
              "id": "5aaad7c5-0a9b-44bd-b0e8-e6312c27a8b0",
              "roles": ["tenantUser"],
              "domains": [
                {
                  "guid": "ba40a4fd-fd4d-4e40-bcb7-6111174b0488",
                  "roles": [],
                  "devicePolicies": []
                },
                {
                  "guid": "0c1f3ac0-7ba8-45be-90a8-14fc4ac801dd",
                  "roles": [],
                  "devicePolicies": []
                }
              ]
            }
          ]
        }
      ],
      "attributeMappings": [
        {"enable": true, "name": "Username",    "mappingAttribute": "uid;samaccountname"},
        {"enable": true, "name": "First Name",  "mappingAttribute": "givenName"},
        {"enable": true, "name": "Last Name",   "mappingAttribute": "sn"},
        {"enable": true, "name": "Email",       "mappingAttribute": "mail"},
        {"enable": true, "name": "Description", "mappingAttribute": "description"},
        {"enable": true, "name": "Phone Number","mappingAttribute": "homePhone"}
      ],
      "advancedSettings": ""
    },
    "id": "b144d33d-455f-41c0-8fcb-54f0def583d0",
    "alias": "192.168.31.168",
    "desc": "",
    "type": 2,
    "enabled": true,
    "testUserName": "xxxx@netbraintech.com",
    "testPassword": "Netbrain1123"
  }'
```

