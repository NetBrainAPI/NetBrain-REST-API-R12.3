
# Network Setting API Design

## ***GET*** /V1/CMDB/NetworkSettings/All
This API is used to get All Network Settings of the domain, including Front Server, Jumpbox, SNMP String, Private Key, Telnet/SSH Login, and Privilege Login

## Detail Information

> **Title** : Get All Network Settings API<br>

> **Version** : 29/01/2026.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/NetworkSettings/All

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Path Parameters(****required***)  
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|type|string|The type of Network Settings:<br>telnetInfo |

## Parameters 
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
| token | string  | Authentication token, get from login API. |

## Response

|**Name**|**Type**|**Corresponding UI tabs**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|frontServer | array of objects  | Front Server |
|jumpbox | array of objects  | Jumpbox |
|snmpInfo | array of objects  | SNMP String |
|sshPrivateKey  | array of objects  | Private Key |
|telnetInfo  | array of objects  | Telnet/SSH Login |
|privilegeInfo  | array of objects  | Privilege Login |
|statusCode| int | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |

# Full Example:
```python
full_url = nb_url + "/ServicesAPI/API/V1/CMDB/NetworkSettings/All"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}

headers["Token"]=token

try:
    response = requests.get(full_url, headers=headers, verify=False)
    if response.status_code == 200:
        result = response.json()
        print(result)
    else:
        print("Failed to Get All Network Settings! - " + response.text)
except Exception as e:
    print(str(e))
```
```python
{
  "settings": {
    "privilegeInfo": [
      {
        "ID": "netbrain",
        "enableUserName": "",
        "refCount": 10,
        "alias": "netbrain",
        "enablePassword": "",
        "order": 0
      }
    ],
    "jumpbox": [
      {
        "ID": "Jumpbox",
        "quitCmd": "exit",
        "loginPrompt": "login:",
        "mode": 1,
        "userId": "",
        "commandPrompt": "#",
        "telnetCommand": "telnet $(IP) $(PORT)",
        "enablePrompt": "",
        "port": 22,
        "enableCmd": "",
        "enablePassword": "",
        "isChangeEnablePassword": false,
        "yesNoPrompt": "(yes/no)?",
        "ipAddr": "10.10.5.141",
        "alias": "Jumpbox",
        "password": "",
        "isChangePassword": false,
        "type": 100,
        "name": "",
        "SSHKeyId": "",
        "SSHCommand": "ssh -l $(USERNAME) -p $(PORT) $(IP)",
        "enablePasswordPrompt": "",
        "userName": "root",
        "passwordPrompt": "password:",
        "refCount": 0,
        "order": 0
      }
    ],
    "snmpInfo": [
      {
        "ID": "nb",
        "snmpPort": 0,
        "roString": "",
        "isChangeRoString": false,
        "alias": "nb",
        "snmpVersion": 1,
        "refCount": 26,
        "order": 0
      }
    ],
    "sshPrivateKey": [
      {
        "ID": "nopass",
        "md5KeyContent": "",
        "keyContent": "",
        "passwordPhrase": "",
        "keyName": "RSA2048.ppk",
        "alias": "nopass",
        "refCount": 0,
        "order": 0
      }
    ],
    "telnetInfo": [
      {
        "ID": "netbrain",
        "userName": "netbrain",
        "alias": "netbrain",
        "cliMode": 0,
        "sshKeyID": "0",
        "password": "",
        "decodeChallengeEnable": false,
        "decodeChallengePrivateKeyID": "",
        "refCount": 10,
        "order": 0
      }
      {
        "ID": "netscreen",
        "userName": "netscreen",
        "alias": "netscreen",
        "cliMode": 0,
        "sshKeyID": "",
        "password": "",
        "decodeChallengeEnable": false,
        "decodeChallengePrivateKeyID": "",
        "refCount": 0,
        "order": 25
      }
    ],
    "frontServer": [
      {
        "id": "FS2",
        "alias": "localhost",
        "ipOrHostname": "192.168.28.18",
        "key": "",
        "registered": true,
        "tenantInfo": {
          "id": "4cab3cc8-81e7-f4ce-ce1d-df056e9eff8e",
          "name": "Patch_Tenant"
        },
        "isFSG": false,
        "refCount": 0,
        "refAMCount": 0,
        "refAPIServerCount": 0,
        "refAPIServerAMCount": 0,
        "order": 2,
        "tsRegistered": "2021-08-20T14:46:31Z",
        "ID": "FS2"
      }
    ]
  },
  "statusCode": 790200,
  "statusDescription": "Success."
}
```
# cURL Code from Postman
```python
curl -X GET \
  'http://192.168.28.44/ServicesAPI/API/V1/CMDB/NetworkSettings/All' \
  -H "Content-Type: application/json"
  -H 'cache-control: no-cache' \
  -H 'token: e798fe18-eb94-4b2e-87dc-31ba6b332f93'
```