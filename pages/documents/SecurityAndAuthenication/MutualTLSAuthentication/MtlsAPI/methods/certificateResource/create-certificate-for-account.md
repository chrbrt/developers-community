---
pagename: Create certificate for account
redirect_from:
  - xxx.html
keywords:
sitesection: Documents
categoryname: "Security & Authenication"
documentname: MTLS API
subfoldername: Methods
---

This API creates certificate for specific account id.

### Request

 |Method|      URL|  
 |:--------  |:---  |
 |POST|  https://[{domain}]/mtls/account/{accountId}/certificates |


**Request Headers**

 |Header         |Description  |
 |:------|        :--------  |
 |Authorization|    Contains token string to allow request authentication and authorization.  |

**Request Body**
```
[
{
	"name":"myCert1",
	"p12":[98,121,116,101,115, ...],
	"password":"paw1"
}
]
```

**Path Parameters**

 |Parameter|  Description|  Type/Value |
 |:------    |:--------    |:--------|
 |accountId|  LP site ID |   String |

### Response

**Response Codes** 

| Code | Description           |
|------|-----------------------|
| 201  | Created               |
| 401  | Not Authenticated     |
| 403  | Not Authorized        |
| 500  | Internal Server Error |


**Response Headers**

**Response Body**

for example:
    
```
{  
   "successfulySavedCertificates":[  
      {  
         "id":2628739923,
         "deleted":false,
         "name":"{certificateName}",
         "displayName":"{certificateName}",
         "siteId":"{accountId}",
         "status":"Available",
	 "expirationDate": null
      }
   ],
   "failedSaveToVaultCertificates":[  

   ]
}
```



**Entity Structure:**

| Attribute | Description  | Type/Value | Required | Notes |
| :------   | :--------    | :-------- | :--- | :--- |
| id | A certificate's unique object ID in account config table. | long number | Read only | |
| deleted   | Indicates whether the certificate is deleted or not. | Boolean | Read only | |
| name | A certificate's unique name. | unique string | Required | |
| displayName    | A certificate's display name.  | string | Required | |
| siteId | A site ID of the certificate. | string | Required | |
| status | Indicates if the certificate is available/not available/expired | string | Required | (the certificate is available if it exists at both Hashicorp Vault and DB and if isn't expired)|
| expirationDate | certificate's expiration date. | string | Not Required | |
