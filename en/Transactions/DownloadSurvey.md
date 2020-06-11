
# Download Survey Report

Returns an Inspection Stop Survey Report containing all the information gathered during the inspection process and includes and images/photos taken.

The response message will contain the raw file content. The response won't contain any xml or json encoded information

**URL** : `/api/OutboundStop/DownloadSurvey`

**Method** : `Get`

**Auth **Required**** : YES

**Headers**

| Key | Value |
|--------------|--------------|
| Accept | application/pdf |
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

The file name can be extarcted from the custom Response Header with the following key.

### Response Custom Header
| Key | Value |
|--------------|--------------|
| x-filename | {fileName}.pdf |


```http

HTTP/1.1 200 OK
Content-Type: application/pdf
Content-Disposition: attachment; INDEPENDENT_CARGO_SURVEY_REPORT#xxxxx.pdf
x-filename: "INDEPENDENT_CARGO_SURVEY_REPORT#xxxxx.pdf"

{RAW-PDF-CONTENT}

```


## Response *Failed*
**Result** : `false`

**Content Example**

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: text/plain
{Inspection Stop not found based on input parameter}
```
