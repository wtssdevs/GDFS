
# Get Status Events

Retrieves a list of status events for a stop inspection request. 


**URL** : `/api/OutBoundStop/UploadStopFiles`

**Method** : `POST`

**Auth **Required**** : YES

**Headers**

| Key | Value |
|--------------|--------------|
| Content-Type | application/json  |
| Accept | application/json |3
| Authorization | Bearer + AccessToken received from Authenticate Response Result |

*(Example: “Bearer yJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi...”)*


### Stop File Data model
| Type| Params| Values| Validation |
|--------------|---------- |-------------- |------------ |
|StopFileDto|fileAsBase64String|string [max]|**Required**|
|StopFileDto|mimeType|string [150]|**Required**|
|StopFileDto|fileName|string [150]|**Required**|
|StopFileDto|MovementReferenceNumber|string [18]|*Conditional **Required**|
|StopFileDto|TransactionRefId|number|*Conditional **Required**|



**Body Raw (application/json)**

**Content Example**

```json
[
    {
        "fileAsBase64String": "JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdGFsb2cvUGL1ZpZXdlclByZW=...",
        "mimeType": "application/pdf",
        "fileName": "TT01.pdf",
        "movementReferenceNumber": "JSA201908285075236",
        "transactionRefId": ""
    },
    {
        "fileAsBase64String": "JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdGFsb2cvUGFnZXMgMiAwIFIvT=...",
        "mimeType": "application/pdf",
        "fileName": "TT02.pdf",
        "movementReferenceNumber": "",
        "transactionRefId": "4526"
    }
]
```

## Response *Success* 
**Success** : `true`

**Content Example**

```json
{
    "result": null,
    "targetUrl": null,
    "success": true,
    "error": null,
    "unAuthorizedRequest": false,
    "__abp": true
}

```


## Response *Failed*
**Result** : `false`

**Content Example**

```json
{
    "result": null,
    "targetUrl": null,
    "success": false,
    "error": {
        "code": 404,
        "message": "Transaction not found",
        "details": "Resource not found",
        "validationErrors": null
    },
    "unAuthorizedRequest": false,
    "__abp": true
}
```
