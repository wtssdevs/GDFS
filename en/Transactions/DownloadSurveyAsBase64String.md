
# Download Survey Report

Returns an Inspection Stop Survey Report containing all the information gathered during the inspection process and includes and images/photos taken.

The response message will contain the file content as Base64 String inside a JSON object.

**URL** : `/api/OutboundStop/DownloadSurveyAsBase64String`

**Method** : `Get`

**Auth **Required**** : YES

**Headers**

| Key | Value |
|--------------|--------------|
| Accept | application/json |
| Authorization | Bearer + AccessToken received from Authenticate Response Result |
| Cache-Control | no-cache |


*(Example: “Bearer yJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi...”)*


### URL Query Params
| Key| Value| Type| Validation |
|--------------|---------- |-------------- |------------ |
|TransactionRefId|XXXX|number|**Required**|


**URL Query String**

**Content Example**

```http
GET /api/OutboundStop/DownloadSurvey?transactionRefId=3000 
HTTP/1.1
Authorization: Bearer eyJhbGciOiJA...

```

## Response *Success* 
**Success** : `true`

**Content Example**

```json
{
    "result": {
        "surveyAsBase64String": "JVBERi0xLjQNCiWio4+TDQo1IDAgb2JqDQo8PC9UeXB......",
        "fileName": "INDEPENDENT_CARGO_SURVEY_REPORT#xxxxx.pdf",
        "mimeType": "application/pdf"
    },
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
    "result": "Inspection Stop not found based on input parameter",
    "targetUrl": null,
    "success": false,
    "error": {
        "code": 422,
        "message": "Unprocessable Entity",
        "details": "Inspection Stop not found based on input parameter!",
        "validationErrors": null
    },
    "unAuthorizedRequest": false,
    "__abp": true
}

```
