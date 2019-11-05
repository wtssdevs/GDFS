
# Upload Stop Inspection Files

Upload Supporting Documents/Files releated to the Inspection Stop after it has been created.


**URL** : `/api/InboundStop/UploadStopFiles`

**Method** : `POST`

**Headers**

| Key | Value |
|--------------|--------------|
| Content-Type | application/json  |
| Accept | application/json |


### Stop File Data model
| Type| Params| Values| Validation |
|--------------|---------- |-------------- |------------ |
|StopFileDto|fileAsBase64String|string [max]|**Required**|
|StopFileDto|mimeType|string [150]|**Required**|
|StopFileDto|fileName|string [150]|**Required**|
|StopFileDto|MovementReferenceNumber|string [18]|*Conditional **Required**|
|StopFileDto|TransactionRefId|number|*Conditional **Required**|

*
> **MovementReferenceNumber**  Conditional **Required** (When MovementReferenceNumber is NULL or Empty then TransactionRefId Becomes Required.)
> **TransactionRefId**  Conditional **Required** When TransactionRefId is NULL or Empty then MovementReferenceNumber Becomes Required.

**Body Raw (application/json)**

**Content Example**

```json
{
    "userNameOrEmailAddress": "UserName",
    "password": "password123",
    "rememberClient": true
}
```

## Response *Success* 
**Success** : `true`

**Content Example**

```json
[
    {
        "fileAsBase64String": "JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdGFsb2cvUGL1ZpZXdlclByZW=...",
        "mimeType": "application/pdf",
        "fileName": "TT01.pdf",
        "MovementReferenceNumber": "JSA201908285075236",
        "TransactionRefId": ""
    },
    {
        "fileAsBase64String": "JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdGFsb2cvUGFnZXMgMiAwIFIvT=...",
        "mimeType": "application/pdf",
        "fileName": "TT02.pdf",
        "MovementReferenceNumber": "",
        "TransactionRefId": "4526"
    }
]
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

