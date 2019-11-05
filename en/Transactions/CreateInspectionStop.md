
# Create Stop (Inspection Request)

Creates a New Inspection Stop.

**URL** : `/api/InboundStop/Create`

**Method** : `POST`

**Headers**

| Key | Value |
|--------------|--------------|
| Content-Type | application/json  |
| Accept | application/json |
| Authorization | Bearer + Token received from Authenticate |

## (Example: “Bearer yJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi...”)

### Stop Data Model
**Data constraints**

| Type| Params| Values| Validation |
|--------------|---------- |-------------- |------------ |
|BasicStopDto|StopType|Enum (0)|**Required**|
|BasicStopDto|FileRefNo|string [150]|Optional|
|BasicStopDto|CaseNumber|string [150]|Optional|
|BasicStopDto|MasterAirWaybillNo|string [150]|Optional|
|BasicStopDto|HouseAirWaybillNo|string [150]|Optional|
|BasicStopDto|FlightDateTime|DateTime|Optional|
|BasicStopDto|Consignee|string [150]|Optional|
|BasicStopDto|Warehouse|string [150]|Optional|
|BasicStopDto|FlightNumber|string [150]|Optional|
|BasicStopDto|ReferenceNo|string [150]|Optional|
|BasicStopDto|Depot|string [150]|Optional|
|BasicStopDto|MovementReferenceNumber|string [18]|*Conditional **Required**|
|BasicStopDto|BillOfEntryNo|string [150]|*Conditional **Required**|
|BasicStopDto|BillOfEntryDate|DateTime|Optional|
|BasicStopDto|PortHealthRefNo|string [150]|Optional|
|BasicStopDto|ContainerNo|string [11]|Optional|
|BasicStopDto|FCLGRP|string [150]|Optional|
|BasicStopDto|PCKT|string [150]|Optional|
|BasicStopDto|Weight|number (double)|Optional|
|BasicStopDto|BranchCode|string [150]|**Required**|
|BasicStopDto|AgentCode|string [150]|**Required**|
|BasicStopDto|StopFiles|array [StopFileDto]|Optional|

*
> **MovementReferenceNumber**  Conditional **Required** (When MovementReferenceNumber is NULL or Empty then BillOfEntryNo Becomes Required.)
The MRN number is made up of Customs office code eg. JSA
Customs Bill of Entry date and Assessment date eg 20190828
Lastly the bill of entry no eg 5075236
Full MRN number would be JSA201908285075236

> **BillOfEntryNo**  Conditional **Required** When BillOfEntryNo is NULL or Empty then MovementReferenceNumber Becomes Required.

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

**Content Example StopType Enum**

```json

"stopType": {
    "type": "number",        
    "enum": [{"SeaFreight": 0}, {"AirFreight": 1}]
}

```

**Content Example Without Files**

```json
{
    "stopType": 1, 
    "fileRefNo": "Test",
    "caseNumber": "123456",
    "masterAirWaybillNo": "083-1234567",
    "houseAirWaybillNo": "House1",
    "flightDateTime":"2019-08-26T23:05:09.9159514+02:00" ,
    "consignee": "",
    "warehouse": "",
    "flightNumber": "FL12345",
    "MovementReferenceNumber":"JSA201908285075236",
    "depot": "",
    "referenceNo": "",
    "billOfEntryNo": "",
    "billOfEntryDate": "",
    "portHealthRefNo": "",
    "containerNo": "",
    "fclgrp": "",
    "pckt": "",
    "weight": 25,
    "branchCode": "PTA",
    "agentCode": "DFG00149AS2",
    "stopFiles": [] 
}
```

## Response *Success* 
**Success** : `true`

**Content Example**

```json

{
    "result": {
        "TransactionRefId": 4526, //BigInt
        "TransactionNo": "SDFR19054526", //string [30]
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
    "result": null,
    "targetUrl": null,
    "success": false,
    "error": {
        "code": 422,
        "message": "Your request is not valid!",
        "details": "The following errors were detected during validation. - The field Code must be a string with a maximum length of 50.",
        "validationErrors": [
            {
                "message": "The field Code must be a string with a maximum length of 50.",
                "members": [
                    "code"
                ]
            }
        ]
    },
}

```

**Content Example With Files**

```json
{
    "stopType": 1, 
    "fileRefNo": "Test",
    "caseNumber": "123456",
    "masterAirWaybillNo": "083-1234567",
    "houseAirWaybillNo": "House1",
    "flightDateTime":"2019-08-26T23:05:09.9159514+02:00" ,
    "consignee": "",
    "warehouse": "",
    "flightNumber": "FL12345",
    "MovementReferenceNumber":"JSA201908285075236",
    "depot": "",
    "referenceNo": "",
    "billOfEntryNo": "",
    "billOfEntryDate": "",
    "portHealthRefNo": "",
    "containerNo": "",
    "fclgrp": "",
    "pckt": "",
    "weight": 25,
    "branchCode": "PTA",
    "agentCode": "DFG00149AS2",
    "stopFiles": [
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
}

```

## Response *Success* 
**Success** : `true`

**Content Example**

```json

{
    "result": {
        "TransactionRefId": 4526, //BigInt
        "TransactionNo": "SDFR19054526", //string [30]
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
    "result": null,
    "targetUrl": null,
    "success": false,
    "error": {
        "code": 422,
        "message": "Your request is not valid!",
        "details": "The following errors were detected during validation. - The field Code must be a string with a maximum length of 50.",
        "validationErrors": [
            {
                "message": "The field Code must be a string with a maximum length of 50.",
                "members": [
                    "code"
                ]
            }
        ]
    },
}

```

